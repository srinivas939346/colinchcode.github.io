---
layout: post
title: "[python] Querying data using Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Tortoise ORM is an asynchronous Python ORM (Object Relational Mapping) framework that provides an easy and intuitive way to interact with databases.

In this blog post, we will explore how to query data using Tortoise ORM in Python.

## Table of Contents
- [Installation](#installation)
- [Connecting to the Database](#connecting-to-the-database)
- [Defining Models](#defining-models)
- [Querying Data](#querying-data)
  - [Basic Query](#basic-query)
  - [Filtering](#filtering)
  - [Ordering](#ordering)
  - [Limiting](#limiting)
  - [Joining Tables](#joining-tables)
  - [Aggregates](#aggregates)
- [Conclusion](#conclusion)

## Installation
First, we need to install Tortoise ORM. You can install it using pip:

```shell
pip install tortoise-orm
```

## Connecting to the Database
To connect to a database, we need to define the database configuration. For example, to connect to a SQLite database, create a `conf.py` file with the following content:

```python
from tortoise import Tortoise

DB_URL = "sqlite://db.sqlite3"

Tortoise.init(
    db_url=DB_URL,
    modules={"models": ["path.to.models"]}
)
```

Make sure to replace "path.to.models" with the actual path to your models.

## Defining Models
Tortoise ORM uses models to interact with the database. Let's create a simple `User` model to demonstrate querying:

```python
from tortoise import fields
from tortoise.models import Model


class User(Model):
    id = fields.IntField(pk=True)
    name = fields.CharField(max_length=255)
    email = fields.CharField(max_length=255, unique=True)
    created_at = fields.DatetimeField(auto_now_add=True)

    def __str__(self):
        return self.name
```

## Querying Data
Now that we have our database connection and model defined, let's dive into querying data.

### Basic Query
To retrieve all users from the database, we can use the `all()` method:

```python
users = await User.all()
for user in users:
    print(user.name)
```

### Filtering
We can filter the results based on specific conditions using the `filter()` method:

```python
filtered_users = await User.filter(name="John")
for user in filtered_users:
    print(user.email)
```

### Ordering
To order the results, we can use the `order_by()` method:

```python
ordered_users = await User.order_by("-created_at")
for user in ordered_users:
    print(user.name)
```

### Limiting
To limit the number of results returned, we can use the `limit()` method:

```python
limited_users = await User.limit(5)
for user in limited_users:
    print(user.name)
```

### Joining Tables
Tortoise ORM supports joining tables to retrieve related data. Let's consider a scenario where a `User` has a foreign key relationship with a `Post` model:

```python
class Post(Model):
    id = fields.IntField(pk=True)
    title = fields.CharField(max_length=255)
    content = fields.TextField()
    user = fields.ForeignKeyField("models.User", related_name="posts")

    def __str__(self):
        return self.title

# Retrieve all posts with the associated user's name
posts = await Post.all().values(User__name="user__name")
for post in posts:
    print(post["User__name"], post.title)
```

### Aggregates
Tortoise ORM also supports aggregate functions like `count()`, `sum()`, `avg()`, etc. Here's an example of using the `count()` function:

```python
users_count = await User.all().count()
print(users_count)
```

These are just a few examples of how to query data using Tortoise ORM. You can find more information and examples in the [official documentation](https://tortoise-orm.readthedocs.io/en/latest/).

## Conclusion
Tortoise ORM provides a powerful and intuitive way to query data from databases using Python. With its rich set of features, it makes working with databases hassle-free. Whether you are building a small project or a large-scale application, Tortoise ORM can simplify your data querying tasks. Give it a try and experience its efficiency and flexibility.