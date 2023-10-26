---
layout: post
title: "[python] Creating a Flask application with SQLAlchemy integration"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Flask is a popular web framework in Python, and SQLAlchemy is a powerful Object-Relational Mapping (ORM) tool. Combining these two technologies allows us to build robust and scalable web applications. In this blog post, we will explore how to create a Flask application with SQLAlchemy integration.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Setting up the Flask Application](#setting-up-the-flask-application)
- [Setting up the Database](#setting-up-the-database)
- [Defining Models](#defining-models)
- [Using SQLAlchemy in Routes](#using-sqlalchemy-in-routes)
- [Conclusion](#conclusion)

## Prerequisites
Before we get started, make sure you have the following installed:
- Python (version 3 or above)
- Flask (`pip install flask`)
- SQLAlchemy (`pip install SQLAlchemy`)

## Setting up the Flask Application
First, let's create a new directory for our Flask application and navigate into it. Create a new Python file called `app.py`:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return 'Hello, Flask!'
    
if __name__ == '__main__':
    app.run()
```

Save the file and run it using the command `python app.py`. Open a web browser and navigate to `http://localhost:5000`. You should see the message "Hello, Flask!" displayed.

## Setting up the Database
To use SQLAlchemy, we need to connect our Flask application to a database. For this example, we will use SQLite. Update `app.py` with the following code:

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///database.db'
db = SQLAlchemy(app)

@app.route('/')
def hello():
    return 'Hello, Flask!'

if __name__ == '__main__':
    app.run()
```

Run the application again, and SQLAlchemy will automatically create a `database.db` file in the same directory.

## Defining Models
Now, let's define our database models using SQLAlchemy. Add the following code to `app.py`:

```python
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(50), unique=True, nullable=False)
    email = db.Column(db.String(120), unique=True, nullable=False)
    
    def __repr__(self):
        return f'<User {self.username}>'
```

This creates a `User` class that inherits from `db.Model`. It defines three columns: `id`, `username`, and `email`. The `__repr__` method returns a string representation of the user object, which is useful for debugging.

Run the application again, and SQLAlchemy will create a `users` table in the database.

## Using SQLAlchemy in Routes
We can now use SQLAlchemy to interact with the database in our routes. Update `app.py` with the following code:

```python
from flask import Flask, render_template, request, redirect
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///database.db'
db = SQLAlchemy(app)

@app.route('/')
def hello():
    users = User.query.all()
    return render_template('index.html', users=users)

@app.route('/add', methods=['POST'])
def add():
    username = request.form['username']
    email = request.form['email']
    user = User(username=username, email=email)
    db.session.add(user)
    db.session.commit()
    return redirect('/')

if __name__ == '__main__':
    app.run()
```

In this example, we import the `render_template`, `request`, and `redirect` functions from Flask. We query all users from the `User` table and pass them to the `index.html` template. We also define a route `/add` to handle adding new users to the database.

Create an `index.html` file in the same directory as `app.py`:

```html
{% raw %}
<!DOCTYPE html>
<html>
<head>
    <title>Flask SQLAlchemy Example</title>
</head>
<body>
    <h1>Users</h1>
    <ul>
        {% for user in users %}
        <li>{{ user.username }} - {{ user.email }}</li>
        {% endfor %}
    </ul>
    <h2>Add User</h2>
    <form action="/add" method="post">
        <label>Username:</label>
        <input type="text" name="username" required>
        <br>
        <label>Email:</label>
        <input type="text" name="email" required>
        <br>
        <input type="submit" value="Add">
    </form>
</body>
</html>
{% endraw %}
```

Restart the application and navigate to `http://localhost:5000`. You should see a list of users and a form to add new users. Submit the form, and the user will be added to the database.

## Conclusion
In this blog post, we have learned how to create a Flask application with SQLAlchemy integration. We set up the Flask application, connected it to a SQLite database, defined models using SQLAlchemy, and used SQLAlchemy in routes to interact with the database. By combining Flask and SQLAlchemy, you can build powerful web applications with ease.