---
layout: post
title: "[python] Managing database migrations with Flask-Migrate and SQLAlchemy"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When working on a Flask application that uses SQLAlchemy as the ORM (Object-Relational Mapping) tool, one important aspect to consider is database migrations. Database migrations allow you to make changes to your database schema over time while preserving existing data. Flask-Migrate is a popular extension that simplifies the process of managing database migrations in a Flask application. In this article, we will explore how to use Flask-Migrate and SQLAlchemy for database migrations.

## Table of Contents
- [Setting up Flask-Migrate](#setting-up-flask-migrate)
- [Defining database models](#defining-database-models)
- [Creating and applying migrations](#creating-and-applying-migrations)
- [Rolling back migrations](#rolling-back-migrations)
- [Conclusion](#conclusion)

## Setting up Flask-Migrate

To get started with Flask-Migrate, you need to install the package using pip:

```bash
pip install Flask-Migrate
```

Flask-Migrate requires SQLAlchemy and Flask as dependencies, so make sure you have them installed as well.

Next, you need to initialize Flask-Migrate in your Flask application. Create a Python module (e.g., `migrations.py`) where you will initialize the extension:

```python
# migrations.py

from flask import Flask
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'your_database_uri'

db = SQLAlchemy(app)
migrate = Migrate(app, db)
```

Make sure to replace `'your_database_uri'` with the actual URI for your database.

## Defining database models

Database models in SQLAlchemy are typically defined using classes. Each class represents a table in the database, and attributes of the class represent columns. Here's an example of a simple user table:

```python
# models.py

from migrations import db

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(80), unique=True, nullable=False)
    email = db.Column(db.String(120), unique=True, nullable=False)

    def __repr__(self):
        return f'<User {self.username}>'
```

In this example, we import the `db` instance from `migrations.py` and use it to define the `User` model. The `id`, `username`, and `email` attributes represent the columns in the `user` table. The `__repr__` method provides a string representation of the model object.

## Creating and applying migrations

Once you have defined your database models, you can create the initial migration using the following command:

```bash
flask db init
```

This will create a `migrations` directory in your project, which will contain the migration scripts. To generate a migration script based on the changes you made to the models, run the following command:

```bash
flask db migrate -m "initial migration"
```

The `-m` option allows you to provide a message for the migration, which is helpful for keeping track of the changes made in each migration.

Finally, to apply the migration and update the database schema, run the following command:

```bash
flask db upgrade
```

This will execute the migration script and apply the changes to the database.

## Rolling back migrations

If you need to roll back a migration and revert the changes to the previous state, you can use the following command:

```bash
flask db downgrade
```

This will undo the last applied migration.

## Conclusion

Managing database migrations is an essential part of developing Flask applications with SQLAlchemy. Flask-Migrate provides a convenient and straightforward way to create and apply migrations, allowing for easy maintenance and modifications to the database schema. By following the steps outlined in this article, you can effectively manage your database migrations and keep your application's data in-sync with the evolving schema.