---
layout: post
title: "[python] Filtering data using Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Tortoise ORM is an easy-to-use asyncio ORM with support for both SQL databases and NoSQL databases. It allows you to interact with databases using Python code in an efficient and convenient way.

Filtering data is a common requirement when working with databases. In this blog post, we will explore how to filter data using Tortoise ORM with Python.

## Table of Contents
- [Installing Tortoise ORM](#installing-tortoise-orm)
- [Connecting to the Database](#connecting-to-the-database)
- [Filtering Data](#filtering-data)
- [Combining Filters](#combining-filters)
- [Conclusion](#conclusion)
- [References](#references)

## Installing Tortoise ORM

To get started, you need to install Tortoise ORM. You can do this using pip:

```shell
pip install tortoise-orm
```

## Connecting to the Database

Before we can start filtering data, we need to establish a connection to the database. Tortoise ORM supports various databases including SQLite, PostgreSQL, and MySQL. For this example, we will assume a SQLite database.

```python
from tortoise import Tortoise

async def connect_to_database():
    await Tortoise.init(
        db_url='sqlite://db.sqlite3',
        modules={'models': ['your_module.models']}
    )
    await Tortoise.generate_schemas()

async def disconnect_from_database():
    await Tortoise.close_connections()
```

## Filtering Data

Tortoise ORM provides a rich set of methods to filter data. Let's say we have a `User` model with `name` and `age` fields. Here's an example of filtering users based on their age:

```python
from your_module.models import User

async def filter_users_by_age(min_age, max_age):
    users = await User.filter(age__gte=min_age, age__lte=max_age).all()
    return users
```

In the example above, we use the `filter` method to specify our filter criteria. The `age__gte` and `age__lte` are called lookup operators. `gte` stands for "greater than or equal to" and `lte` stands for "less than or equal to". This filters the users with ages between `min_age` and `max_age`.

## Combining Filters

Tortoise ORM supports combining multiple filters using logical operators like `AND` and `OR`. Here's an example:

```python
from your_module.models import User

async def filter_users_by_age_and_name(min_age, max_age, name):
    users = await User.filter(age__gte=min_age, age__lte=max_age, name__icontains=name).all()
    return users
```

In this example, we add an additional filter to find users with a specific name. We use the `name__icontains` lookup operator, which performs a case-insensitive match of the name field.

## Conclusion

Filtering data is an essential operation when working with databases. In this blog post, we have learned how to filter data using Tortoise ORM with Python. We explored various filtering options and combining filters to refine our queries.

Tortoise ORM simplifies the process of filtering data, enabling you to work with databases efficiently and conveniently. Using the methods provided by Tortoise ORM, you can easily build complex queries to retrieve the data you need.

## References

- [Tortoise ORM documentation](https://tortoise-orm.readthedocs.io/)
- [Tortoise ORM GitHub repository](https://github.com/tortoise/tortoise-orm)