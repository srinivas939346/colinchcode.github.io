---
layout: post
title: "[python] Defining database models using SQLAlchemy in Flask"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In Flask, SQLAlchemy is a popular and powerful toolkit used to interact with databases. It provides an Object-Relational Mapping (ORM) system that allows developers to define their database models using Python classes and interact with the database using object-oriented methods.

In this article, we will explore how to define database models using SQLAlchemy in Flask and perform basic database operations.

## Table of Contents
1. [Installation](#installation)
2. [Defining the database models](#defining-the-database-models)
3. [Creating the database tables](#creating-the-database-tables)
4. [Performing basic database operations](#performing-basic-database-operations)
5. [Conclusion](#conclusion)

## Installation
First, we need to install the required libraries. You can install SQLAlchemy and Flask-SQLAlchemy using pip by running the following commands:

```python
pip install SQLAlchemy
pip install Flask-SQLAlchemy
```

## Defining the database models
To define a database model in SQLAlchemy, we need to create a Python class that inherits from the `db.Model` class provided by Flask-SQLAlchemy. Each attribute in the class represents a column in the corresponding database table.

Here's an example of a simple database model for a blog post:

```python
from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()

class Post(db.Model):
    __tablename__ = 'posts'
    id = db.Column(db.Integer, primary_key=True)
    title = db.Column(db.String(255))
    content = db.Column(db.Text)
    created_at = db.Column(db.DateTime, default=db.func.current_timestamp())
```

In the above code snippet, we import the `SQLAlchemy` class from `flask_sqlalchemy` module and create an instance of it called `db`. This `db` instance will be used to interact with the database.

The `Post` class represents a table named 'posts'. It has columns such as `id`, `title`, `content`, and `created_at`. We define the column types using `db.Column` and provide additional parameters like primary key, string length, text, and default values.

## Creating the database tables
To create the database tables based on the defined models, we need to call the `create_all()` method on the `db` object. This method will inspect the defined models and generate the necessary SQL statements to create the tables.

Here's an example of how to create the tables:

```python
from your_flask_app import app, db

# ...

with app.app_context():
    db.create_all()
```

In the above code snippet, we import the Flask app and the `db` object from our Flask-SQLAlchemy instance. Then, we use the `app.app_context()` to make the application context active and call the `create_all()` method to create the tables.

## Performing basic database operations
Once the tables are created, we can perform basic database operations such as inserting, updating, and deleting records.

### Inserting records
To insert a new record into the database table, we can create a new object of the model class and add it to the database session:

```python
new_post = Post(title="New Post", content="This is a new blog post.")
db.session.add(new_post)
db.session.commit()
```

In the above code snippet, we create a `new_post` object with the desired values, add it to the session using `db.session.add()`, and finally commit the changes using `db.session.commit()`.

### Querying records
To query records from the database table, we can use the `query` attribute provided by the model class:

```python
all_posts = Post.query.all()
```

The `query.all()` method returns a list of all the records in the table.

### Updating records
To update an existing record, we can retrieve the object from the database, modify its attributes, and commit the changes:

```python
post = Post.query.get(1)
post.title = "Updated Post"
db.session.commit()
```

In the above code snippet, we retrieve the object with `id` equal to 1 using `query.get()`, update its `title` attribute, and commit the changes using `db.session.commit()`.

### Deleting records
To delete a record from the database table, we can retrieve the object and call the `delete()` method:

```python
post = Post.query.get(1)
db.session.delete(post)
db.session.commit()
```

In the above code snippet, we retrieve the object with `id` equal to 1, delete it from the session using `db.session.delete()`, and commit the changes using `db.session.commit()`.

## Conclusion
In this article, we have learned how to define database models using SQLAlchemy in Flask and perform basic database operations such as inserting, querying, updating, and deleting records. SQLAlchemy provides a convenient and expressive way to interact with databases, allowing developers to focus more on the application logic rather than dealing with low-level SQL operations.

Remember to check the official documentation of SQLAlchemy and Flask-SQLAlchemy for more information and advanced usage.