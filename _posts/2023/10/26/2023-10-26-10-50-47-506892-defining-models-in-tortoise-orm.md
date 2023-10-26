---
layout: post
title: "[python] Defining models in Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Tortoise ORM is an easy-to-use Python ORM (Object Relational Mapping) for working with databases. It provides a simple and intuitive way to define models and interact with the database. In this article, we will explore how to define models in Tortoise ORM.

### Installation

Before we dive into defining models, make sure you have installed Tortoise ORM. You can install it using pip:

``` python
pip install tortoise-orm
```

### Creating a connection

To interact with a database using Tortoise ORM, you need to establish a connection. The connection string contains the details required to connect to the database such as the host, port, username, password, and database name. Here's an example of how to create a connection to a PostgreSQL database:

``` python
from tortoise import Tortoise, fields

async def init():
    await Tortoise.init(
        db_url='postgres://username:password@localhost:5432/mydatabase',
        modules={'models': ['your_module_name.models']}
    )
    await Tortoise.generate_schemas()

async def close():
    await Tortoise.close_connections()
```

### Defining a model

To define a model in Tortoise ORM, you need to create a class that inherits from the `tortoise.models.Model` class. Properties of the model are defined as class attributes. Each property represents a field in the database table.

``` python
from tortoise.models import Model
from tortoise import fields

class User(Model):
    id = fields.IntField(pk=True)
    username = fields.CharField(max_length=50)
    email = fields.CharField(max_length=100, unique=True)
    created_at = fields.DatetimeField(auto_now_add=True)
```

In the example above, we define a `User` model with four properties: `id`, `username`, `email`, and `created_at`. The `id` property is an integer field and is marked as the primary key (`pk=True`). The `username` and `email` properties are character fields with specified maximum lengths. The `created_at` field is a datetime field that automatically sets the value to the current datetime when a new instance is created.

### Defining relationships

Tortoise ORM supports defining relationships between models. You can define one-to-one, one-to-many, and many-to-many relationships using different field types.

``` python
from tortoise import fields, models

class User(models.Model):
    id = fields.IntField(pk=True)
    username = fields.CharField(max_length=50)
    articles = fields.ReverseRelation['Article']

class Article(models.Model):
    id = fields.IntField(pk=True)
    title = fields.CharField(max_length=100)
    user = fields.ForeignKeyField('models.User', related_name='articles')
```

In the example above, we define a one-to-many relationship between the `User` and `Article` models. The `User` model has a `ReverseRelation` field named `articles`, which represents the relationship from `User` to `Article`. The `Article` model has a foreign key field named `user`, which represents the relationship from `Article` to `User`.

### Conclusion

Defining models in Tortoise ORM is straightforward and allows you to easily interact with your database. With the flexibility to define relationships between models, Tortoise ORM provides a powerful tool for working with databases in Python.

For more information, refer to the [Tortoise ORM documentation](https://tortoise-orm.readthedocs.io/).