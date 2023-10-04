---
layout: post
title: "[python] Defining Database Models in SQLAlchemy"
description: " "
date: 2023-10-04
tags: [python]
comments: true
share: true
---

When working with databases in Python, SQLAlchemy is a popular and powerful library that provides an object-relational mapping (ORM) system. SQLAlchemy allows us to define and interact with database models using Python classes, making it easier to manage and manipulate data.

In this blog post, we will explore how to define database models in SQLAlchemy and perform basic database operations using these models.

## Table of Contents
- [Introduction to SQLAlchemy](#introduction-to-sqlalchemy)
- [Defining Models](#defining-models)
- [Creating Tables](#creating-tables)
- [Inserting Data](#inserting-data)
- [Retrieving Data](#retrieving-data)
- [Updating Data](#updating-data)
- [Deleting Data](#deleting-data)
- [Conclusion](#conclusion)

## Introduction to SQLAlchemy

SQLAlchemy is an open-source SQL toolkit and object-relational mapping library for Python. It provides a set of high-level API for organizing and managing database operations. SQLAlchemy supports various database systems including PostgreSQL, MySQL, SQLite, and more.

To start using SQLAlchemy, you need to install it using `pip`:

```shell
$ pip install SQLAlchemy
```

Once installed, you can import SQLAlchemy in your Python script or application:

```python
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.orm import sessionmaker
from sqlalchemy.ext.declarative import declarative_base
```

## Defining Models

In SQLAlchemy, a model represents a table in the database. We define a model by creating a class that inherits from the `declarative_base()` object. Each attribute of the class represents a column in the table.

Here's an example of defining a simple model for a `User` table:

```python
Base = declarative_base()

class User(Base):
    __tablename__ = 'users'

    id = Column(Integer, primary_key=True)
    name = Column(String)
    email = Column(String)
```

In the above example, we define a `User` model with three columns: `id`, `name`, and `email`. The `__tablename__` attribute specifies the name of the table in the database.

## Creating Tables

To create the tables corresponding to our models, we need to create an engine and call the `create_all()` method on the `Base` object. The engine represents the connection to the database.

```python
engine = create_engine('sqlite:///database.db')
Base.metadata.create_all(engine)
```

The above code creates the necessary tables in an SQLite database named `database.db`. You can replace the database URL with your own database connection string.

## Inserting Data

To insert data into the database, we first create an instance of our model and set the attribute values. We then add the instance to a session and commit the changes.

```python
Session = sessionmaker(bind=engine)
session = Session()

user = User(name='John Doe', email='john@example.com')
session.add(user)
session.commit()
```

The above code inserts a new user into the `users` table. We create a session using the sessionmaker and bind it to the engine. We then create a new `User` instance, set the attribute values, add it to the session, and finally commit the changes.

## Retrieving Data

To retrieve data from the database, we can use the `query()` method of the session. This method allows us to perform various queries using SQLAlchemy's query API.

```python
users = session.query(User).all()
```

The above code retrieves all the users from the `users` table. We use the `query()` method and pass the `User` model as an argument. The `all()` method returns all the records as a list.

## Updating Data

To update data in the database, we first retrieve the record we want to update, modify the attributes, and then commit the changes.

```python
user = session.query(User).filter_by(name='John Doe').first()
user.email = 'john.doe@example.com'
session.commit()
```

The above code updates the email address of a user with the name 'John Doe'. We use the `query()` method with a filter condition to retrieve the specific user, modify the email attribute, and commit the changes.

## Deleting Data

To delete data from the database, we can use the `query()` method to retrieve the record and then call the `delete()` method on it.

```python
user = session.query(User).filter_by(name='John Doe').first()
session.delete(user)
session.commit()
```

The above code deletes a user from the database. We use the `query()` method with a filter condition to retrieve the specific user, call the `delete()` method, and commit the changes.

## Conclusion

In this blog post, we explored how to define database models in SQLAlchemy and perform basic database operations using these models. SQLAlchemy provides a convenient and intuitive way to work with databases in Python, allowing us to focus on the logic of our applications rather than dealing with low-level SQL operations.

For more advanced use cases, SQLAlchemy offers a rich set of features and capabilities that can handle complex database scenarios. Check out the official SQLAlchemy documentation for more information and examples. Happy coding!