---
layout: post
title: "[python] SQLAlchemy and Flask Integration"
description: " "
date: 2023-10-04
tags: [python]
comments: true
share: true
---

When building web applications with Flask, integrating a database system is often a requirement. One popular choice for working with databases in Flask is SQLAlchemy. SQLAlchemy is an Object Relational Mapping (ORM) library that provides a high-level interface to interact with relational databases. In this blog post, we will explore how to integrate SQLAlchemy with Flask and perform basic database operations.

## Prerequisites

Before we begin, make sure you have Flask and SQLAlchemy installed in your Python environment. You can install them using pip:

```python
pip install flask sqlalchemy
```

## Setting up the Database

First, let's set up a SQLite database for our example application. Create a new file called `app.db` in your project directory. We will use this database to store our application's data.

## Initializing the Flask Application

To integrate SQLAlchemy with Flask, we need to initialize the Flask application with SQLAlchemy. In your Flask application's main file (e.g., `app.py`), import the necessary modules:

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy
```

Next, create an instance of the Flask app:

```python
app = Flask(__name__)
```

Now, let's configure the database connection. Add the following configuration to your Flask app:

```python
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///app.db'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
```

The `SQLALCHEMY_DATABASE_URI` setting specifies the connection URL for the SQLite database. In this case, we use a SQLite database located in the `app.db` file. The `SQLALCHEMY_TRACK_MODIFICATIONS` setting is set to `False` to disable modification tracking, which improves performance.

Finally, initialize the SQLAlchemy extension with your Flask app:

```python
db = SQLAlchemy(app)
```

## Creating a Model

In SQLAlchemy, a database table is represented by a Python class, known as a model. Let's create a simple `User` model to represent users in our application. Below is an example of a user model:

```python
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(50), unique=True, nullable=False)
    email = db.Column(db.String(120), unique=True, nullable=False)

    def __repr__(self):
        return f'<User {self.username}>'
```

In this example, we define three columns: `id`, `username`, and `email`. The `id` column is the primary key, and both `username` and `email` columns are defined as unique and not nullable. The `__repr__` method is used to display a user object in a human-readable format.

## Creating and Accessing Data

To create a new user record in the database, we can use the following code:

```python
new_user = User(username='john', email='john@example.com')
db.session.add(new_user)
db.session.commit()
```

In this example, we create a new `User` instance with a username and email address and add it to the session. The `db.session.commit()` method saves the changes and persists the new user record in the database.

To query the user records from the database, we can use the following code:

```python
users = User.query.all()
```

This will retrieve all the user records from the `User` table and store them in the `users` list. You can then iterate through the list and access the user attributes as needed.

## Updating and Deleting Data

To update an existing user record, you can modify the attributes of the user object and call `db.session.commit()`:

```python
user = User.query.get(1)
user.username = 'new_username'
db.session.commit()
```

To delete a user record, you can use the following code:

```python
user = User.query.get(1)
db.session.delete(user)
db.session.commit()
```

## Conclusion

In this blog post, we explored how to integrate SQLAlchemy with Flask and perform basic database operations. SQLAlchemy provides a powerful and flexible way to interact with databases in Flask applications. By utilizing SQLAlchemy, you can focus on the logic of your application while letting SQLAlchemy handle the database operations efficiently.