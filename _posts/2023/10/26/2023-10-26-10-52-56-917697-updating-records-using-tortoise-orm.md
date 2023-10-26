---
layout: post
title: "[python] Updating records using Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Tortoise ORM is an easy-to-use ORM (Object Relational Mapping) library for asynchronous databases in Python. It provides a simple and intuitive way to interact with databases and perform operations like updating records. In this tutorial, we will explore how to update records using Tortoise ORM in Python.

## Table of Contents
- [Installation](#installation)
- [Connecting to the Database](#connecting-to-the-database)
- [Updating Records](#updating-records)
- [Summary](#summary)

## Installation

Before we start, we need to install Tortoise ORM. You can install it using pip with the following command:

```python
pip install tortoise-orm
```

Make sure you have a compatible database driver installed as well. Tortoise ORM supports various databases such as PostgreSQL, MySQL, SQLite, and others. You'll need to install the appropriate database driver depending on your database system.

## Connecting to the Database

To connect to the database, we need to define the database configuration in `tortoise_config.py` file. Here's an example of connecting to a PostgreSQL database:

```python
from tortoise import Tortoise

DB_CONFIG = {
    'connections': {
        'default': {
            'engine': 'tortoise.backends.asyncpg',
            'credentials': {
                'database': 'your_database',
                'host': 'localhost',
                'port': '5432',
                'user': 'your_username',
                'password': 'your_password'
            }
        }
    },
    'apps': {
        'models': {
            'models': ['your_app.models'],
            'default_connection': 'default'
        }
    }
}

Tortoise.init(config=DB_CONFIG)
```

Replace `your_database`, `your_username`, and `your_password` with your actual database credentials.

## Updating Records

To update records using Tortoise ORM, follow these steps:

1. Import the necessary models and fields from Tortoise ORM.
2. Use the `update()` method to modify the desired record(s).
3. Use `save()` method to save the changes to the database.

Here's an example to update a record in a `User` model:

```python
from tortoise import Model, fields

class User(Model):
    id = fields.IntField(pk=True)
    username = fields.CharField(max_length=255)
    email = fields.CharField(max_length=255)

    async def update_user(self, new_username):
        self.username = new_username
        await self.save()

# Update a user record
async def update_user_record(user_id, new_username):
    user = await User.get(id=user_id)
    await user.update_user(new_username)
```

In this example, we define a `User` model with `id`, `username`, and `email` fields. The `update_user()` method updates the `username` field and saves the changes to the database using the `save()` method.

To update a specific record, we fetch the user using the `get()` method and then call the `update_user()` method with the new username.

## Summary

In this tutorial, we explored how to update records using Tortoise ORM in Python. We covered the installation process, connecting to the database, and updating records in a model using Tortoise ORM's `update()` and `save()` methods. Tortoise ORM makes it convenient to work with databases and simplifies the process of updating records in Python applications.