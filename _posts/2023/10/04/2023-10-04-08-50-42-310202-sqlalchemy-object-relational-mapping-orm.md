---
layout: post
title: "[python] SQLAlchemy Object Relational Mapping (ORM)"
description: " "
date: 2023-10-04
tags: [python]
comments: true
share: true
---

In this blog post, we will explore SQLAlchemy, which is a Python tool for working with databases using an Object-Relational Mapping (ORM) approach. SQLAlchemy provides a convenient and powerful way to interact with databases without having to write raw SQL queries.

## What is Object-Relational Mapping (ORM)?

Object-Relational Mapping is a technique that allows developers to map database tables to classes and automatically generate SQL queries based on the defined mappings. ORM provides an abstraction layer between application logic and database operations, making it easier to work with databases and reducing the amount of boilerplate code.

## Why use SQLAlchemy ORM?

There are several benefits of using the SQLAlchemy ORM:

1. **Database independence**: SQLAlchemy supports multiple database backends including SQLite, PostgreSQL, MySQL, and more. You can switch between different databases without changing the code significantly.

2. **Simplified querying**: SQLAlchemy provides a high-level API for writing database queries. It abstracts the underlying SQL language and allows you to write queries using Python constructs.

3. **Automatic table creation**: SQLAlchemy can automatically create database tables based on your defined models. This makes it easier to set up the initial database schema.

4. **Data integrity and relationships**: SQLAlchemy ORM allows you to define relationships between tables using object references. It handles the complexity of joining tables and ensures data integrity.

Now let's dive into some practical examples of using SQLAlchemy ORM.

## Installation

First, you need to install SQLAlchemy using pip:

```python
pip install SQLAlchemy
```

## Connecting to a Database

To connect to a database, we need to create an engine object that represents the database connection. SQLAlchemy supports various database engines such as SQLite, PostgreSQL, and MySQL. Here's an example of connecting to an SQLite database:

```python
from sqlalchemy import create_engine

engine = create_engine('sqlite:///mydatabase.db')
```

## Defining Models

In SQLAlchemy, a model is a Python class that represents a database table. Each attribute of the class corresponds to a column in the table. Here's an example of defining a simple `User` model:

```python
from sqlalchemy import Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

class User(Base):
    __tablename__ = 'users'
    
    id = Column(Integer, primary_key=True)
    name = Column(String)
    email = Column(String, unique=True)
```

## CRUD Operations

Once you have defined your models, you can perform CRUD (Create, Read, Update, Delete) operations using SQLAlchemy ORM. Here are some examples:

- **Create** a new user:

```python
new_user = User(name='John Doe', email='johndoe@example.com')
session.add(new_user)
session.commit()
```

- **Read** users from the database:

```python
users = session.query(User).all()
for user in users:
    print(user.name, user.email)
```

- **Update** a user:

```python
user = session.query(User).filter_by(email='johndoe@example.com').first()
user.name = 'John Smith'
session.commit()
```

- **Delete** a user:

```python
user = session.query(User).filter_by(email='johndoe@example.com').first()
session.delete(user)
session.commit()
```

In addition to CRUD operations, SQLAlchemy ORM provides advanced features such as querying with conditions, aggregations, and joins. You can explore the official SQLAlchemy documentation for more information.

## Conclusion

SQLAlchemy ORM is a powerful tool for working with databases in Python. It provides an easy-to-use API for defining models, performing CRUD operations, and handling relationships between tables. Using SQLAlchemy ORM allows you to focus on your application logic without worrying about the low-level details of working with databases.