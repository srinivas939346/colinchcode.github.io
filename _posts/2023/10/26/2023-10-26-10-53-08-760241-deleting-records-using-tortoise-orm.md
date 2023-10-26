---
layout: post
title: "[python] Deleting records using Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

## Table of Contents

- [Introduction](#introduction)
- [Deleting Records](#deleting-records)
- [Conclusion](#conclusion)

## Introduction

Tortoise ORM is an easy-to-use and async ORM for Python. It provides a simple way to interact with databases and perform CRUD operations. In this blog post, we will focus on the **delete** operation.

## Deleting Records

To delete records using Tortoise ORM, we need to follow a few steps:

1. Import the necessary modules:
```python
from tortoise import Tortoise
from tortoise.models import Model
from tortoise import fields
```

2. Define a model that represents the table where you want to perform the deletion. Here's an example of a `User` model with a name field:
```python
class User(Model):
    id = fields.IntField(pk=True)
    name = fields.CharField(max_length=255)
```

3. Initialize the Tortoise ORM:
```python
Tortoise.init_models(['path.to.models']) # Replace 'path.to.models' with the actual path to your models
Tortoise.init_db(dsn='sqlite://:memory:', modules={'models': ['path.to.models']}) # Replace 'path.to.models' with the actual path to your models
```

4. Perform the deletion using the `delete` method of the Tortoise queryset:
```python
async def delete_users():
    await User.filter(id=1).delete()
```

5. Execute the deletion function:
```python
await delete_users()
```

In the example above, we are deleting a user with an `id` of 1. You can modify the `filter` method to specify the criteria for deletion.

## Conclusion

Deleting records using Tortoise ORM is a straightforward process. By following the steps mentioned in this blog post, you can easily delete records from your database tables. Make sure to read the documentation of Tortoise ORM for more advanced features and options.

For more information, you can refer to the official Tortoise ORM documentation at [https://tortoise-orm.readthedocs.io/](https://tortoise-orm.readthedocs.io/).

Happy coding!