---
layout: post
title: "[python] Retrieving a single record using Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In this blog post, we will discuss how to retrieve a single record from a database using Tortoise ORM in Python.

## Table of Contents
1. [Introduction to Tortoise ORM](#introduction-to-tortoise-orm)
2. [Retrieving a Single Record](#retrieving-a-single-record)
3. [Example Code](#example-code)
4. [Conclusion](#conclusion)
5. [References](#references)

## Introduction to Tortoise ORM
Tortoise ORM is an easy-to-use asynchronous ORM (Object Relational Mapping) library for Python that provides a straightforward way to interact with databases. It supports various database backends such as PostgreSQL, MySQL, SQLite, and others.

## Retrieving a Single Record
To retrieve a single record from a database using Tortoise ORM, we can utilize the `get` method. The `get` method allows us to query the database based on specified conditions and return a single record matching those conditions.

In order to use Tortoise ORM, make sure you have it installed in your Python environment. You can install it using pip:

```python
pip install tortoise-orm
```

## Example Code
Let's consider a simple example where we have a "User" model representing a user in a database. We can retrieve a single user record by calling the `get` method on the model and providing a condition.

```python
from tortoise import Tortoise, fields, models


class User(models.Model):
    username = fields.CharField(max_length=255)
    email = fields.CharField(max_length=255)

async def retrieve_user(username):
    user = await User.get(username=username)
    return user

async def main():
    await Tortoise.init(db_url="sqlite://db.sqlite3", modules={"models": ["__main__"]})
    await Tortoise.generate_schemas()
    
    user = await retrieve_user("john123")
    print(user.username, user.email)
    
    await Tortoise.close_connections()

if __name__ == "__main__":
    await main()
```

In this example, we create a `User` model with fields for username and email. The `retrieve_user` function takes a username as an argument and retrieves the user record from the database using the `get` method.

We initialize the Tortoise ORM, generate the database schema, retrieve the user with the username "john123", and print the username and email of the retrieved user.

## Conclusion
Retrieving a single record from a database using Tortoise ORM is straightforward. By using the `get` method, we can query the database based on specified conditions and retrieve a single record matching those conditions.

Tortoise ORM provides a convenient and efficient way to interact with databases in Python, making database operations easier to manage and maintain.

## References
- Tortoise ORM documentation: [https://tortoise-orm.readthedocs.io](https://tortoise-orm.readthedocs.io)