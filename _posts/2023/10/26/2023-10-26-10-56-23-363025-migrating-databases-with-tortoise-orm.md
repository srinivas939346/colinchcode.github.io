---
layout: post
title: "[python] Migrating databases with Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to migrate databases using Tortoise ORM, a powerful asynchronous Python ORM (Object-Relational Mapping) library. 

### Table of Contents

1. [Introduction to Tortoise ORM](#introduction)
2. [Setting up a Database Connection](#connection)
3. [Creating Migrations](#migrations)
4. [Applying Migrations](#applying)
5. [Rolling Back Migrations](#rollback)
6. [Conclusion](#conclusion)

### 1. Introduction to Tortoise ORM<a name="introduction"></a>

Tortoise ORM is an easy-to-use ORM for Python 3.6+ that provides a simple and intuitive way to interact with databases. It supports popular databases like Postgres, MySQL, and SQLite.

Tortoise ORM follows an asynchronous approach, making it suitable for high-performance applications that require concurrency. It also offers built-in support for migrations, allowing developers to manage database schema changes effortlessly.

### 2. Setting up a Database Connection<a name="connection"></a>

To get started with Tortoise ORM, you need to establish a connection with your desired database. Here's an example of how to set up a connection using Tortoise ORM in Python:

```python
from tortoise import Tortoise

async def connect_to_database():
    await Tortoise.init(
        db_url='sqlite://mydatabase.db',
        modules={'models': ['app.models']}
    )
    await Tortoise.generate_schemas()

# Run the connection setup
connect_to_database()
```

In the code snippet above, we import `Tortoise` and use the `init()` method to specify the database URL and the modules containing the models. Finally, the `generate_schemas()` method is called to create the necessary tables in the database.

### 3. Creating Migrations<a name="migrations"></a>

Once the database connection is established, Tortoise ORM allows you to define and create migrations for your database schema changes. Migrations are written as Python classes and provide a way to version control your database schema.

Here's an example of a migration file `0001_initial.py`:

```python
from tortoise import fields, models

class Product(models.Model):
    id = fields.IntField(pk=True)
    name = fields.CharField(max_length=255)
    price = fields.DecimalField(max_digits=8, decimal_places=2)
```

In the above example, we define a model `Product` with three fields: `id`, `name`, and `price`. The `id` field is assigned as the primary key using `pk=True`. 

### 4. Applying Migrations<a name="applying"></a>

To apply the migrations to the database, we can use the Tortoise ORM command-line interface (CLI) tool. 

```
tortoise-orm migrate --name app.migrations
```

In the above command, we specify the `--name` flag followed by the path to the migrations module (`app.migrations`). This command will apply any pending migrations to the database.

### 5. Rolling Back Migrations<a name="rollback"></a>

Tortoise ORM also provides the ability to rollback migrations if needed. To rollback the most recent migration, you can use the following command:

```
tortoise-orm rollback --name app.migrations
```

This command will revert the last applied migration and bring the database schema back to its previous state.

### 6. Conclusion<a name="conclusion"></a>

In this blog post, we explored how to migrate databases using Tortoise ORM. We started by setting up a database connection and then created migrations for schema changes. We learned how to apply migrations to the database and rollback migrations if needed.

Tortoise ORM simplifies the process of managing database migrations, making it easier to handle changes to your database schema. It's a powerful tool for developers working on Python projects that require database operations.

To learn more about Tortoise ORM and its features, refer to the official documentation: [Tortoise ORM Documentation](https://tortoise-orm.readthedocs.io/)

Happy migrating!