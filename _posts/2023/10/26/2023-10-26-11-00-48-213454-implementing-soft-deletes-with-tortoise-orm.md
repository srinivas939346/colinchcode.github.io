---
layout: post
title: "[python] Implementing soft deletes with Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In data-driven applications, it is often necessary to handle the deletion of data in a way that allows for easy recovery or auditing. Soft deletes provide a solution by flagging records as "deleted" instead of physically removing them from the database. 

In this article, we will explore how to implement soft deletes using the Tortoise ORM, a powerful async ORM for Python.

## Table of Contents

1. [Introduction](#introduction)
2. [Setting up Tortoise ORM](#setup-tortoise-orm)
3. [Implementing Soft Deletes](#implementing-soft-deletes)
4. [Retrieving Deleted Records](#retrieving-deleted-records)
5. [Conclusion](#conclusion)

## Introduction<a name="introduction"></a>

Soft deletes allow you to keep track of deleted records by adding an extra field to your database table. This field typically consists of a boolean flag or a timestamp, indicating whether the record has been deleted.

Tortoise ORM provides a straightforward way of implementing soft deletes with its built-in support for fields and models.

## Setting up Tortoise ORM<a name="setup-tortoise-orm"></a>

Before we dive into implementing soft deletes, let's first set up our project with Tortoise ORM.

First, install Tortoise ORM using `pip`:

```python
pip install tortoise-orm
```

Next, create a `models.py` file and import the necessary modules:

```python
from tortoise.models import Model
from tortoise import fields
```

Now, let's define a sample model to work with:

```python
class User(Model):
    id = fields.IntField(pk=True)
    name = fields.CharField(max_length=255)

    class Meta:
        table = "users"
```

This model represents a user with an `id` field and a `name` field.

To connect to our database, we need to configure a database URL and call the `Tortoise.init()` method:

```python
Tortoise.init(
    db_url="sqlite://db.sqlite3",
    modules={"models": ["models"]},
)
```

With the Tortoise ORM set up, we can now proceed to implement soft deletes.

## Implementing Soft Deletes<a name="implementing-soft-deletes"></a>

To implement soft deletes, we will add a `deleted` field to our model and override the `delete` method to handle the soft deletion logic.

First, add the `deleted` field to your model:

```python
class User(Model):
    id = fields.IntField(pk=True)
    name = fields.CharField(max_length=255)
    deleted = fields.BooleanField(default=False)

    class Meta:
        table = "users"
```

Now, let's override the `delete` method to update the `deleted` field instead of actually deleting the record:

```python
class User(Model):
    id = fields.IntField(pk=True)
    name = fields.CharField(max_length=255)
    deleted = fields.BooleanField(default=False)

    class Meta:
        table = "users"

    async def delete(self):
        self.deleted = True
        await self.save()
```

With this modification, calling the `delete` method on a `User` instance will update the `deleted` field to `True`. The record will still exist in the database with the `deleted` flag set to `True`.

## Retrieving Deleted Records<a name="retrieving-deleted-records"></a>

To retrieve soft-deleted records, we can use a custom query filter. Let's add a `deleted_users` method to our `User` model:

```python
class User(Model):
    id = fields.IntField(pk=True)
    name = fields.CharField(max_length=255)
    deleted = fields.BooleanField(default=False)

    class Meta:
        table = "users"

    async def delete(self):
        self.deleted = True
        await self.save()

    @classmethod
    async def deleted_users(cls):
        return cls.filter(deleted=True)
```

Now, calling `User.deleted_users()` will return a queryset containing all soft-deleted users.

## Conclusion<a name="conclusion"></a>

Soft deletes provide a convenient way to handle deleted data in a more flexible and controlled manner. With the help of Tortoise ORM, implementing soft deletes is straightforward and allows for easy recovery or auditing of deleted records.

By following the steps outlined in this article, you should now have a good understanding of how to implement soft deletes using Tortoise ORM in your Python projects.

Further reading:
- Tortoise ORM documentation: [https://tortoise-orm.readthedocs.io](https://tortoise-orm.readthedocs.io)
- Soft delete pattern: [https://martinfowler.com/eaaCatalog/softDelete.html](https://martinfowler.com/eaaCatalog/softDelete.html)