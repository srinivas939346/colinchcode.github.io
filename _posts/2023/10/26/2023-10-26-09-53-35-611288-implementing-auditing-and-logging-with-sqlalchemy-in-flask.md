---
layout: post
title: "[python] Implementing auditing and logging with SQLAlchemy in Flask"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In a Flask application, it is important to keep track of actions performed by users and to log any errors or important events that occur. SQLAlchemy, a popular Object-Relational Mapping (ORM) library, can be used to implement auditing and logging functionalities. In this blog post, we will explore how to integrate SQLAlchemy with Flask to achieve this.

## Table of Contents
1. [Setting up the Flask application](#setup)
2. [Configuring SQLAlchemy](#config)
3. [Implementing auditing](#auditing)
4. [Implementing logging](#logging)
5. [Conclusion](#conclusion)

## Setting up the Flask application <a name="setup"></a>

To get started, let's create a basic Flask application. First, make sure you have Flask installed:

```python
pip install flask
```

Create a new file `app.py` and add the following code:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run()
```

Run the Flask application:

```python
python app.py
```

Navigate to `http://localhost:5000` in your browser, and you should see the message "Hello, World!".

## Configuring SQLAlchemy <a name="config"></a>

Next, let's configure SQLAlchemy to work with our Flask application. First, install SQLAlchemy:

```python
pip install sqlalchemy
```

In `app.py`, import SQLAlchemy and configure it as follows:

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///db.sqlite'
db = SQLAlchemy(app)

@app.route('/')
def index():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run()
```

Create a new file `models.py` and define a sample model:

```python
from app import db

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(50), unique=True)

    def __repr__(self):
        return '<User %r>' % self.username
```

To create the SQLite database, open a Python shell and execute the following commands:

```python
from app import db
from models import User

db.create_all()
```

## Implementing auditing <a name="auditing"></a>

To implement auditing, we can use SQLAlchemy's event system to listen for changes made to the model objects. For example, let's log any new user created in the `User` model.

Add the following code to `models.py`:

```python
from app import db
from datetime import datetime

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(50), unique=True)
    created_at = db.Column(db.DateTime, default=datetime.utcnow)

    def __repr__(self):
        return '<User %r>' % self.username

@db.event.listens_for(User, 'after_insert')
def log_user_creation(mapper, connection, target):
    print(f"User '{target.username}' created at {target.created_at}.")
```

Now, when a new user is created, the `log_user_creation` function will be called, printing a log message with the username and creation timestamp.

## Implementing logging <a name="logging"></a>

To implement logging, we can use the built-in `logging` module in Python. Let's log any errors that occur in our Flask application.

In `app.py`, import the `logging` module and configure it:

```python
import logging

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///db.sqlite'
db = SQLAlchemy(app)

# Configure logging
logging.basicConfig(filename='error.log', level=logging.ERROR)

@app.errorhandler(Exception)
def handle_exception(error):
    app.logger.error('An error occurred: %s', error)
    return 'An error occurred.', 500

@app.route('/')
def index():
    raise Exception('Oops! Something went wrong.')

if __name__ == '__main__':
    app.run()
```

Now, when an exception occurs, it will be logged to the `error.log` file.

## Conclusion <a name="conclusion"></a>

By integrating SQLAlchemy with Flask, we can easily implement auditing and logging functionalities in our application. We've explored how to configure SQLAlchemy, implement auditing using SQLAlchemy's event system, and log errors using the `logging` module. These practices can help in tracking user actions, debugging issues, and improving the overall reliability of your Flask application.

## References
- [Flask documentation](https://flask.palletsprojects.com/)
- [SQLAlchemy documentation](https://docs.sqlalchemy.org/)
- [Python logging module documentation](https://docs.python.org/3/library/logging.html)