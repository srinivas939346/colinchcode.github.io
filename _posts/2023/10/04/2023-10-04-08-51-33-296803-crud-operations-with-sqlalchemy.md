---
layout: post
title: "[python] CRUD Operations with SQLAlchemy"
description: " "
date: 2023-10-04
tags: [python]
comments: true
share: true
---

SQLAlchemy is a popular Object-Relational Mapping (ORM) library for Python that simplifies database communication. It provides a convenient way to interact with databases, using Python code rather than writing raw SQL queries. In this blog post, we will explore the basic **CRUD** (Create, Read, Update, Delete) operations using SQLAlchemy.

## Table of Contents
- [Setup](#setup)
- [Create](#create)
- [Read](#read)
- [Update](#update)
- [Delete](#delete)

<a name="setup"></a>
## Setup

First, let's set up a basic SQLAlchemy connection to a database. We will assume that you have already installed SQLAlchemy and have a database engine configured. 

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

# Set up the database connection
engine = create_engine('your_database_url')
Session = sessionmaker(bind=engine)
session = Session()
```

Replace `'your_database_url'` with the URL or connection string for your database.

<a name="create"></a>
## Create

To create a new entry in the database, we can simply instantiate a new object and add it to the session. SQLAlchemy will handle the necessary SQL statements to insert the data.

```python
from sqlalchemy import Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

# Define a model or table
class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    email = Column(String(50))
    
# Create a new user
new_user = User(name='John Doe', email='john@example.com')
session.add(new_user)
session.commit()
```

The above code creates a new `User` object and adds it to the session. Then, the `commit()` method is called to persist the changes to the database.

<a name="read"></a>
## Read

To retrieve data from the database using SQLAlchemy, we can use the `query` method and the `filter_by` clause to specify the conditions.

```python
# Retrieve a user by id
user = session.query(User).filter_by(id=1).first()
print(f"User: {user.name}, Email: {user.email}")
```

The above code retrieves a user with the id of 1 from the `users` table and prints the user's name and email.

<a name="update"></a>
## Update

To update an existing entry in the database, we can retrieve the object, modify its properties, and call the `commit()` method.

```python
# Retrieve a user
user = session.query(User).filter_by(id=1).first()

# Update the user's email
user.email = 'new_email@example.com'
session.commit()
```

The above code retrieves a user with the id of 1, updates its email address, and saves the changes to the database.

<a name="delete"></a>
## Delete

To delete an entry from the database, we can use the `delete()` method and call the `commit()` method to persist the changes.

```python
# Retrieve a user
user = session.query(User).filter_by(id=1).first()

# Delete the user
session.delete(user)
session.commit()
```

The above code retrieves a user with the id of 1, deletes it from the database, and saves the changes.

## Conclusion

SQLAlchemy is a powerful ORM library that simplifies database operations in Python. In this blog post, we explored the basic CRUD operations - Create, Read, Update, and Delete - using SQLAlchemy. These operations allow us to interact with databases seamlessly, without writing complex SQL queries.