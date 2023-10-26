---
layout: post
title: "[python] Exploring advanced features and extensions of Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

## Table of Contents
- [Introduction](#introduction)
- [Background](#background)
- [Advanced Features](#advanced-features)
  - [1. Query Joins](#query-joins)
  - [2. Transactions](#transactions)
  - [3. Schema Migrations](#schema-migrations)
- [Extensions](#extensions)
  - [1. Tortoise CRUD](#tortoise-crud)
  - [2. Tortoise Contributions](#tortoise-contributions)
- [Conclusion](#conclusion)
- [References](#references)

## Introduction<a name="introduction"></a>
Tortoise ORM is a Python library that provides a simple yet powerful way to interact with databases using async/await syntax. It is built on top of the asyncio framework and aims to be the most developer-friendly ORM for Python applications.

In this blog post, we will explore some of the advanced features and extensions of Tortoise ORM that can enhance your database operations and streamline your workflow.

## Background<a name="background"></a>
Before we dive into the advanced features and extensions, let's quickly recap the basics of Tortoise ORM. With Tortoise ORM, you define your models as regular Python classes, and Tortoise ORM automatically maps those classes to database tables. It supports various database backends, including SQLite, PostgreSQL, and MySQL.

To get started with Tortoise ORM, you need to install it using pip:

`pip install tortoise-orm`

Once installed, you can import the necessary modules and connect to your database.

```python
from tortoise import Model, fields, Tortoise

class User(Model):
    id = fields.IntField(pk=True)
    name = fields.CharField(max_length=100)

async def init_db():
    await Tortoise.init(db_url='sqlite://:memory:', modules={'models': ['app.models']})
    await Tortoise.generate_schemas()

async def main():
    await init_db()
    # Your code here

if __name__ == '__main__':
    import asyncio
    asyncio.run(main())
```

## Advanced Features<a name="advanced-features"></a>
Tortoise ORM provides several advanced features that can help you perform complex database operations efficiently. Let's explore some of these features.

### 1. Query Joins<a name="query-joins"></a>
Tortoise ORM allows you to perform JOIN operations to fetch related data from multiple tables using its query API. You can easily join tables based on foreign key relationships and retrieve the data you need. Here's an example:

```python
users = await User.filter(is_active=True).prefetch_related('posts')
for user in users:
    print(f"User: {user.name}")
    for post in user.posts:
        print(f"Post: {post.title}")
```

In this example, we're fetching all active users and their associated posts using the `prefetch_related()` method. Tortoise ORM automatically generates the appropriate JOIN queries for us in the background.

### 2. Transactions<a name="transactions"></a>
Tortoise ORM supports transactions, allowing you to group multiple database operations into a single atomic unit. This ensures that either all the operations succeed or none of them does. Here's an example:

```python
async def create_user_with_post(user_data, post_data):
    async with Tortoise.get_transaction() as conn:
        user = await User.create(**user_data)
        post_data['user'] = user.id
        post = await Post.create(**post_data)
        await conn.commit()
        return user, post
```

In this example, we're using the `get_transaction()` context manager to start a new transaction. Within the transaction, we create a new user and associate a post with it. If any exception occurs during the transaction, Tortoise ORM automatically rolls back the changes, ensuring data consistency.

### 3. Schema Migrations<a name="schema-migrations"></a>
Tortoise ORM also provides a built-in schema migration system that allows you to manage database schema changes as your application evolves. You can define and apply schema migrations using Tortoise CLI. Here's an example:

```
$ tortoise migrations create init
$ tortoise migrations apply
```

In this example, we create an initial migration called "init" and apply it to the database. Tortoise ORM automatically generates the SQL statements to migrate the schema to the current version.

## Extensions<a name="extensions"></a>
Apart from the advanced features, Tortoise ORM also has a vibrant ecosystem of extensions that can further enhance its functionality. Let's explore a couple of popular extensions.

### 1. Tortoise CRUD<a name="tortoise-crud"></a>
Tortoise CRUD is an extension that provides a set of generic CRUD (Create, Read, Update, Delete) APIs for Tortoise ORM models. It simplifies common CRUD operations by abstracting away the boilerplate code. You can easily install and use it in your application:

```
$ pip install tortoise-crud
```

### 2. Tortoise Contributions<a name="tortoise-contributions"></a>
Tortoise Contributions is an extension that provides additional features and utilities to enhance the development experience with Tortoise ORM. It includes features like JSON field support, case-insensitive filtering, and utility functions for complex queries. You can install and use it in your application:

```
$ pip install tortoise-contrib
```

## Conclusion<a name="conclusion"></a>
Tortoise ORM is a powerful library for Python developers to interact with databases using async/await syntax. In this blog post, we explored some of its advanced features, including query joins, transactions, and schema migrations. We also discovered popular extensions like Tortoise CRUD and Tortoise Contributions that can further enhance its functionality.

Tortoise ORM provides an intuitive and elegant way to work with databases, making it a valuable tool for building robust and scalable applications.

## References<a name="references"></a>
- [Tortoise ORM Documentation](https://tortoise-orm.readthedocs.io/)
- [Tortoise CRUD GitHub Repository](https://github.com/13rac1/tortoise-crud)
- [Tortoise Contributions GitHub Repository](https://github.com/Mint-C/tortoise-contrib)