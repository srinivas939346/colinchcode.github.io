---
layout: post
title: "[python] Creating database tables using Flask-SQLAlchemy"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In this blog post, we will learn how to create database tables using Flask-SQLAlchemy in Python. Flask-SQLAlchemy is a Flask extension that provides a simple way to work with SQLAlchemy, a powerful and popular Object-Relational Mapping (ORM) library.

## Table of Contents

1. [Introduction to Flask-SQLAlchemy](#introduction-to-flask-sqlalchemy)
2. [Setting up the Flask-SQLAlchemy extension](#setting-up-the-flask-sqlalchemy-extension)
3. [Defining models](#defining-models)
4. [Creating database tables](#creating-database-tables)
5. [Conclusion](#conclusion)

## Introduction to Flask-SQLAlchemy

Flask-SQLAlchemy integrates the SQLAlchemy library into Flask applications, providing a convenient and intuitive way to interact with databases. It simplifies the process of defining database models and creating tables.

## Setting up the Flask-SQLAlchemy extension

Before we can start creating database tables, we need to set up the Flask-SQLAlchemy extension in our Flask application. First, make sure you have Flask-SQLAlchemy installed:

```python
pip install flask-sqlalchemy
```

Next, import the necessary modules and create an instance of the `SQLAlchemy` class:

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///example.db'

db = SQLAlchemy(app)
```

In the above code, we import `Flask` and `SQLAlchemy` from their respective modules. We create a Flask instance and configure the `SQLALCHEMY_DATABASE_URI` parameter to specify the URI of the database. In this example, we are using a SQLite database file named `example.db`. Lastly, we create an instance of `SQLAlchemy` and bind it to the Flask application.

## Defining models

Once we have set up the Flask-SQLAlchemy extension, we can define our database models. A model is a Python class that represents a database table. Each attribute of the class corresponds to a column in the table.

For example, let's define a simple `User` model:

```python
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(50), unique=True)
    email = db.Column(db.String(100), unique=True)
```

In the above code, we define a `User` model that has three columns: `id`, `username`, and `email`. The `id` column is of type `Integer` and is specified as the primary key. The `username` and `email` columns are of type `String` and are unique.

## Creating database tables

To create the database tables corresponding to our models, we can use the `create_all()` method provided by Flask-SQLAlchemy. This method creates all the tables defined in our models if they do not already exist.

To create the tables, we can add the following code to our Flask application:

```python
with app.app_context():
    db.create_all()
```

The `app_context()` is a context manager that provides an application context for the database operations. The `create_all()` method creates the tables in the database.

## Conclusion

In this blog post, we learned how to create database tables using Flask-SQLAlchemy in Python. We saw how to set up the Flask-SQLAlchemy extension, define models, and create the tables. Flask-SQLAlchemy provides a convenient way to work with databases in Flask applications, allowing us to focus on building our application logic without worrying about low-level database operations.

If you want to learn more about Flask-SQLAlchemy, you can refer to the [official documentation](https://flask-sqlalchemy.palletsprojects.com/).