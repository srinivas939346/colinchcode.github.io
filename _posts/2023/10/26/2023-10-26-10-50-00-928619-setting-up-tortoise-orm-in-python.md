---
layout: post
title: "[python] Setting up Tortoise ORM in Python"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Tortoise ORM is an easy-to-use and powerful Object-Relational Mapping (ORM) library for Python. It provides a straightforward way to interact with relational databases using Python code. In this tutorial, we will learn how to set up Tortoise ORM in a Python project.

## Table of Contents

1. [Installation](#installation)
2. [Connecting to a Database](#connecting-to-a-database)
3. [Defining Models](#defining-models)
4. [Querying the Database](#querying-the-database)
5. [Conclusion](#conclusion)

## Installation

To get started with Tortoise ORM, we need to install it using pip:

```shell
$ pip install tortoise-orm
```

## Connecting to a Database

Once you have installed Tortoise ORM, you can connect to a database using the `init()` function. This function takes the configuration details of the database as arguments.

```python
from tortoise import Tortoise

async def connect_to_database():
    await Tortoise.init(
        db_url='sqlite://test.db',
        modules={'models': ['path.to.models']}
    )
    await Tortoise.generate_schemas()
```

In the above example, `db_url` specifies the URL of the database. In this case, we are using an SQLite database located at `test.db`. The `modules` argument tells Tortoise ORM where to find the models.

## Defining Models

In Tortoise ORM, models are defined as Python classes that inherit from the `tortoise.models.Model` base class. Each attribute of the model class corresponds to a column in the database table.

```python
from tortoise import fields, models

class User(models.Model):
    name = fields.CharField(max_length=100)
    email = fields.CharField(max_length=100, unique=True)
```

In the above example, we define a `User` model with two attributes: `name` and `email`. The `CharField` specifies that the attributes should be stored as strings in the database.

## Querying the Database

Tortoise ORM provides a rich set of methods to query the database. You can use methods like `get()`, `create()`, `filter()`, etc., to perform CRUD operations.

```python
async def retrieve_users():
    users = await User.all()
    for user in users:
        print(user.name, user.email)
```

In the above example, we use the `all()` method to retrieve all the users from the database. We then iterate over the result and print the name and email of each user.

## Conclusion

In this tutorial, we have seen how to set up Tortoise ORM in a Python project. We learned how to connect to a database, define models, and perform basic CRUD operations. Tortoise ORM simplifies working with databases in Python and provides a clean and intuitive interface for interacting with relational databases.