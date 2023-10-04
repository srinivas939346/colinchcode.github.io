---
layout: post
title: "[python] SQLAlchemy and Flask-SQLAlchemy"
description: " "
date: 2023-10-04
tags: [python]
comments: true
share: true
---

When working with databases in Python, SQLAlchemy is a popular choice due to its flexibility and power. It's an Object Relational Mapper (ORM) that provides a high-level interface for interacting with databases.

Flask-SQLAlchemy is an extension for Flask that integrates SQLAlchemy into a Flask application, simplifying the process of database management and interaction. In this article, we will explore the basics of SQLAlchemy and how Flask-SQLAlchemy enhances the database handling capabilities of Flask.

## Table of Contents
- [Introduction to SQLAlchemy](#introduction-to-sqlalchemy)
- [Getting Started with Flask-SQLAlchemy](#getting-started-with-flask-sqlalchemy)
- [Defining Database Models](#defining-database-models)
- [Performing Database Operations](#performing-database-operations)
- [Conclusion](#conclusion)

## Introduction to SQLAlchemy

SQLAlchemy provides an abstraction layer over databases by mapping database tables to Python classes and allowing you to perform operations on these classes. It supports various database engines, including MySQL, PostgreSQL, SQLite, and Oracle.

With SQLAlchemy, you can define your database models as Python classes, and SQLAlchemy will handle the creation and manipulation of database tables based on these models. It also provides a powerful querying API that simplifies the process of retrieving data from the database.

## Getting Started with Flask-SQLAlchemy

To use Flask-SQLAlchemy in your Flask application, you need to install it first:

```python
pip install Flask-SQLAlchemy
```

Once installed, you can initialize a SQLAlchemy object in your Flask app:

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///mydatabase.db'

db = SQLAlchemy(app)
```

Here, we set the `SQLALCHEMY_DATABASE_URI` configuration option to specify the database connection URL. In this case, we are using SQLite and providing a relative path to the database file.

## Defining Database Models

To define a database model in Flask-SQLAlchemy, you can create a Python class inheriting from the `db.Model` class provided by SQLAlchemy:

```python
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(100), unique=True, nullable=False)
    email = db.Column(db.String(100), unique=True, nullable=False)
```

In this example, we define a `User` model with three columns: `id`, `username`, and `email`. Each column is represented by a class attribute of the model class, specifying the column type and any constraints.

## Performing Database Operations

Flask-SQLAlchemy simplifies database operations by providing an easy-to-use API. Here are some examples of common operations:

```python
# Creating a new user
user = User(username='john', email='john@example.com')
db.session.add(user)
db.session.commit()

# Retrieving all users
users = User.query.all()

# Querying with filters
user = User.query.filter_by(username='john').first()

# Updating a user
user.email = 'johnnew@example.com'
db.session.commit()

# Deleting a user
db.session.delete(user)
db.session.commit()
```

These operations demonstrate how Flask-SQLAlchemy integrates SQLAlchemy's functionality into Flask. The `db.session` object is used to perform database operations, such as adding, querying, updating, and deleting records.

## Conclusion

Flask-SQLAlchemy is a powerful extension that streamlines database management in Flask applications. It leverages the flexibility and features of SQLAlchemy while providing a simplified API for interacting with the database.

In this article, we covered the basics of SQLAlchemy and how Flask-SQLAlchemy enhances the database handling capabilities of Flask. With Flask-SQLAlchemy, you can easily define database models, perform various database operations, and leverage the power of SQLAlchemy in your Flask application.