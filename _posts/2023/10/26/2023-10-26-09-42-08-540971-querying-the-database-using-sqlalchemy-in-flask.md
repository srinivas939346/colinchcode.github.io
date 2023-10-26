---
layout: post
title: "[python] Querying the database using SQLAlchemy in Flask"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

SQLAlchemy is a popular Object-Relational Mapping (ORM) library for Python that provides a convenient way to interact with databases. In this blog post, we will explore how to perform database queries using SQLAlchemy in a Flask application.

## Setting up SQLAlchemy in Flask

First, we need to set up SQLAlchemy in our Flask application. To do this, we should have Flask and SQLAlchemy installed in our development environment. You can install them using pip:

```
$ pip install Flask SQLAlchemy
```

Next, we need to import and configure SQLAlchemy in our Flask application. In the file where we create our Flask app, usually `app.py` or `__init__.py`, we can add the following code:

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql://username:password@localhost/mydatabase'
db = SQLAlchemy(app)
```

Make sure to replace `username`, `password`, and `mydatabase` with your own database credentials.

## Defining a Model

In SQLAlchemy, a database table is represented as a Python class. We define a model class that inherits from `db.Model` provided by SQLAlchemy. Each attribute of the class represents a column in the database table.

Here's an example of defining a model for a `User` table with a name and email column:

```python
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(50), nullable=False)
    email = db.Column(db.String(50), unique=True, nullable=False)
```

## Basic Querying

Once we have defined our model, we can perform various database operations, including querying. SQLAlchemy provides a query API that allows us to construct complex queries using a fluent interface.

Here are some examples of basic querying operations:

### Get all records

To retrieve all records from a table, we can use the `all()` method on the model class:

```python
users = User.query.all()
```

This will return a list of all `User` objects.

### Filter records

To filter records based on certain conditions, we can use the `filter()` method:

```python
users = User.query.filter(User.name == 'John').all()
```

This will retrieve all `User` objects with the name 'John'.

### Limit and offset

To limit the number of records returned or skip a certain number of records, we can use the `limit()` and `offset()` methods:

```python
users = User.query.limit(10).offset(5).all()
```

This will retrieve 10 `User` objects starting from the 6th record.

### Ordering

To order the results based on a particular column, we can use the `order_by()` method:

```python
users = User.query.order_by(User.name).all()
```

This will retrieve all `User` objects ordered by their names in ascending order.

## Conclusion

SQLAlchemy provides a powerful and flexible way to query databases in Flask applications. In this blog post, we learned how to set up SQLAlchemy in Flask and perform basic querying operations. By using SQLAlchemy, we can easily interact with databases and retrieve the data we need for our applications. For more advanced queries, SQLAlchemy offers a wide range of features that we can explore in the official documentation.

References:
- [SQLAlchemy Documentation](https://docs.sqlalchemy.org/)
- [Flask-SQLAlchemy Documentation](https://flask-sqlalchemy.palletsprojects.com/)