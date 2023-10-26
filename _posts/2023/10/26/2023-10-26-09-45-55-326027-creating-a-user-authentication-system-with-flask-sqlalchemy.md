---
layout: post
title: "[python] Creating a user authentication system with Flask-SQLAlchemy"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to create a user authentication system using Flask and SQLAlchemy. Flask is a lightweight web framework in Python, and SQLAlchemy is an Object-Relational Mapping (ORM) library that simplifies database interactions. This combination allows us to quickly and easily build a secure user authentication system for our web applications.

## Table of Contents
1. [Setting Up the Environment](#setting-up-the-environment)
2. [Creating the User Model](#creating-the-user-model)
3. [Implementing User Registration](#implementing-user-registration)
4. [Enabling User Login](#enabling-user-login)
5. [Protecting Routes](#protecting-routes)
6. [Conclusion](#conclusion)

## Setting Up the Environment
To get started, let's create a new Flask project and set up the necessary environment. Make sure you have Python and Flask installed on your machine. You can install Flask using pip:

```bash
$ pip install Flask
```

Next, create a new project directory and navigate to it in your terminal:

```bash
$ mkdir user-authentication-system
$ cd user-authentication-system
```

## Creating the User Model
The first step in building our authentication system is to define the User model. The User model will represent each user in our application and store their username and password securely.

Create a new file called `models.py` and add the following code:

```python
from flask_sqlalchemy import SQLAlchemy
from werkzeug.security import generate_password_hash, check_password_hash

db = SQLAlchemy()

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(50), unique=True, nullable=False)
    password_hash = db.Column(db.String(128), nullable=False)

    def set_password(self, password):
        self.password_hash = generate_password_hash(password)

    def check_password(self, password):
        return check_password_hash(self.password_hash, password)
```

In this code, we import the necessary modules and create a `db` object using SQLAlchemy. We define the `User` class with three columns: `id`, `username`, and `password_hash`. The `set_password` method is used to set the password for a user, and the `check_password` method is used to verify if a password is correct.

## Implementing User Registration
Now that we have our User model defined, let's implement the user registration functionality. We will create a registration form where users can enter their desired username and password.

Create a new file called `routes.py` and add the following code:

```python
from flask import Flask, render_template, request, redirect, flash
from models import db, User

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///user_auth.db'
app.secret_key = 'your_secret_key'
db.init_app(app)

@app.route('/register', methods=['GET', 'POST'])
def register():
    if request.method == 'POST':
        username = request.form['username']
        password = request.form['password']

        user = User.query.filter_by(username=username).first()
        if user:
            flash('Username already exists.')
            return redirect('/register')

        new_user = User(username=username)
        new_user.set_password(password)
        db.session.add(new_user)
        db.session.commit()

        flash('Registration successful. Please log in.')
        return redirect('/login')

    return render_template('register.html')
```

In this code, we define a route `/register` that handles both GET and POST requests. If the request method is POST, we retrieve the submitted username and password from the form. We check if the username already exists in the database and display an error if it does. If the username is unique, we create a new User object, set their password, and commit it to the database.

## Enabling User Login
With the registration functionality in place, let's implement the user login feature. We will create a login form where users can enter their credentials to authenticate themselves.

Add the following code to `routes.py`:

```python
@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        username = request.form['username']
        password = request.form['password']

        user = User.query.filter_by(username=username).first()
        if user and user.check_password(password):
            # Log in the user
            flash('Login successful.')
            return redirect('/protected')

        flash('Invalid username or password.')
        return redirect('/login')

    return render_template('login.html')
```

In this code, we define a route `/login` that handles both GET and POST requests. If the request method is POST, we retrieve the submitted username and password from the form. We query the User table for a matching username and validate the password using the `check_password` method of the User model.

## Protecting Routes
To protect certain routes in our application, we can use Flask's `@login_required` decorator. This decorator ensures that only authenticated users can access the protected routes. Let's implement a protected route that only logged-in users can access.

Add the following code to `routes.py`:

```python
from flask_login import login_required

@app.route('/protected')
@login_required
def protected():
    return 'Protected Route!'

if __name__ == '__main__':
    app.run(debug=True)
```

In this code, we import the `login_required` decorator from Flask-Login. We define a new route `/protected` and decorate it with `@login_required`. This ensures that only authenticated users can access this route. If an unauthenticated user tries to access the protected route, they will be redirected to the login page.

## Conclusion
In this blog post, we explored how to create a user authentication system using Flask and SQLAlchemy. We defined the User model, implemented registration and login functionality, and protected certain routes to ensure only authenticated users can access them. This provides a solid foundation for building secure web applications that require user authentication. Feel free to extend the code to add additional features such as password reset or user profile management.

References:
- [Flask Documentation](https://flask.palletsprojects.com/)
- [SQLAlchemy Documentation](https://docs.sqlalchemy.org/)
- [Flask-Login Documentation](https://flask-login.readthedocs.io/)