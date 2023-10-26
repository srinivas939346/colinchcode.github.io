---
layout: post
title: "[python] Implementing authentication and authorization with Flask-SQLAlchemy"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to implement authentication and authorization using Flask-SQLAlchemy in a Python Flask web application. Authentication is the process of verifying the identity of a user, while authorization deals with granting or denying access to specific resources based on the authenticated user's privileges.

## Table of Contents

1. [Setting up the Flask-SQLAlchemy](#setup)
2. [Creating a User Model](#user-model)
3. [Implementing Authentication](#authentication)
4. [Implementing Authorization](#authorization)
5. [Conclusion](#conclusion)
6. [References](#references)

## 1. Setting up the Flask-SQLAlchemy {#setup}

To begin, we need to install Flask-SQLAlchemy using pip.

```bash
$ pip install Flask-SQLAlchemy
```

Next, we need to set up the Flask-SQLAlchemy extension in our Flask application.

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///app.db'
db = SQLAlchemy(app)
```

## 2. Creating a User Model {#user-model}

Now, let's create a User model that represents our users in the database.

```python
from werkzeug.security import generate_password_hash, check_password_hash

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(80), unique=True, nullable=False)
    password_hash = db.Column(db.String(128), nullable=False)

    def set_password(self, password):
        self.password_hash = generate_password_hash(password)

    def check_password(self, password):
        return check_password_hash(self.password_hash, password)
```

In the above code, we define three columns for our User model: `id` as the primary key, `username` as a unique string, and `password_hash` to store the hashed password. We also define two methods `set_password` and `check_password` to handle password hashing and verification.

## 3. Implementing Authentication {#authentication}

To implement authentication, we need to create routes for login and logout.

```python
from flask import request, session, redirect

@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        username = request.form['username']
        password = request.form['password']
        user = User.query.filter_by(username=username).first()
        if user and user.check_password(password):
            session['user_id'] = user.id
            return redirect('/')
        else:
            return 'Invalid username or password.'
    return '''
        <form method="post">
            <input type="text" name="username" placeholder="Username" required><br>
            <input type="password" name="password" placeholder="Password" required><br>
            <input type="submit" value="Login">
        </form>
    '''

@app.route('/logout')
def logout():
    session.pop('user_id', None)
    return redirect('/login')
```

In the above code, we have a login route that handles both GET and POST requests. For GET requests, it renders a login form, and for POST requests, it validates the credentials and sets the user_id in the session if they are valid. We also have a logout route that removes the user_id from the session.

## 4. Implementing Authorization {#authorization}

To implement authorization, we can use Flask's `@app.before_request` decorator to check if the user is authenticated for each request.

```python
@app.before_request
def require_login():
    if 'user_id' not in session:
        return redirect('/login')
```

In the above code, we use the `before_request` decorator to define a function that checks if the `user_id` is present in the session. If not, it redirects the user to the login page.

To restrict access to certain routes based on the user's privileges, we can define custom decorators.

```python
from functools import wraps
from flask import abort

def admin_required(f):
    @wraps(f)
    def decorated_function(*args, **kwargs):
        if current_user.role != 'admin':
            abort(403)
        return f(*args, **kwargs)
    return decorated_function

@app.route('/admin')
@admin_required
def admin_panel():
    return 'Welcome to the admin panel!'
```

In the above code, we define a `admin_required` decorator that checks if the current user has the 'admin' role. If not, it returns a 403 Forbidden error. We then use this decorator on the `admin_panel` route to require admin privileges to access it.

## 5. Conclusion {#conclusion}

In this blog post, we learned how to implement authentication and authorization using Flask-SQLAlchemy in a Python Flask web application. We created a User model, implemented the necessary routes for login and logout, and demonstrated how to restrict access to certain routes using custom decorators. By implementing authentication and authorization, we can ensure that our application remains secure and only authorized users can access restricted resources.

## 6. References {#references}

- [Flask-SQLAlchemy documentation](https://flask-sqlalchemy.palletsprojects.com/)
- [Flask documentation](https://flask.palletsprojects.com/)