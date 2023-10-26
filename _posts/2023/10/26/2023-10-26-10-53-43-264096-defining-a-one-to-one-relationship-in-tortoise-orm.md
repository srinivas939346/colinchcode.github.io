---
layout: post
title: "[python] Defining a one-to-one relationship in Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In Tortoise ORM, a one-to-one relationship between two database tables can be defined using a ForeignKeyField. The ForeignKeyField allows us to establish a link between two tables and enforce referential integrity.

Here's an example of how to define a one-to-one relationship using Tortoise ORM:

## Prerequisites

Make sure you have Tortoise ORM installed in your Python environment. If not, you can install it by running the following command:

```shell
pip install tortoise-orm
```

## Defining the Models

Let's consider a scenario where we have two models - `User` and `Profile`. Each `User` can have only one `Profile`. Here's how you can define these models:

```python
from tortoise import fields, models


class User(models.Model):
    id = fields.IntField(pk=True)
    username = fields.CharField(max_length=255, unique=True)
    password = fields.CharField(max_length=255)
    profile = fields.OneToOneField('models.Profile')


class Profile(models.Model):
    id = fields.IntField(pk=True)
    full_name = fields.CharField(max_length=255)
    email = fields.CharField(max_length=255)
```

In the `User` model, we define a OneToOneField called `profile` which links to the `Profile` model.

## Creating a One-to-One Relationship

To establish a one-to-one relationship, you need to ensure that each `User` has a corresponding `Profile`. Here's how you can create a one-to-one relationship in Tortoise ORM:

```python
from tortoise import Tortoise, run_async


async def create_user_with_profile():
    await Tortoise.init(db_url='sqlite://:memory:', modules={'models': ['your_module']})
    await Tortoise.generate_schemas()

    user = await User.create(username='john', password='password')
    profile = await Profile.create(full_name='John Doe', email='john@example.com')

    user.profile = profile
    await user.save()

    await Tortoise.close_connections()


run_async(create_user_with_profile())
```

In this example, we create a `User` record and a corresponding `Profile` record. We then assign the `Profile` instance to the `profile` field of the `User` instance. Finally, we save the `User` instance to establish the one-to-one relationship.

## Conclusion

Defining a one-to-one relationship in Tortoise ORM is straightforward using the ForeignKeyField. By linking the models together, you can establish relationships between tables and easily access related data.