---
layout: post
title: "[python] Creating tables using Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Tortoise ORM is an easy-to-use asyncio ORM (Object-Relational Mapping) library for Python. It allows you to interact with databases using Python objects, making database operations seamless and intuitive. In this blog post, we will look at how to create tables using Tortoise ORM.

## Getting Started

Before we start creating tables, make sure you have Tortoise ORM installed. You can install it using pip:

```
pip install tortoise-orm
```

Once you have Tortoise ORM installed, you can start creating your tables.

## Define Models

In Tortoise ORM, tables are represented by models. Each model corresponds to a table in the database, and each field in the model corresponds to a column in the table. To define a model, you need to create a Python class and inherit from the `tortoise.models.Model` class:

```python
from tortoise import fields
from tortoise.models import Model

class User(Model):
    id = fields.IntField(pk=True)
    name = fields.CharField(max_length=255)
    email = fields.CharField(max_length=255, unique=True)
```

In the above example, we define a `User` model with three fields: `id`, `name`, and `email`. The `id` field is defined as an integer primary key field, while the `name` and `email` fields are defined as character fields with a maximum length of 255 characters. The `unique=True` parameter ensures that each email is unique.

## Create Tables

Once you have defined your models, you can use Tortoise ORM to create the corresponding tables in the database. To create the tables, you need to use the `tortoise.run_sync()` function and pass in the `generate_schema()` method of the `tortoise.Tortoise` class:

```python
from tortoise import Tortoise, run_sync

async def create_tables():
    await Tortoise.init(db_url='sqlite://db.sqlite3', modules={'models': ['app.models']})
    await Tortoise.generate_sche