---
layout: post
title: "[python] Using database triggers with Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to use database triggers with Tortoise ORM, a powerful asynchronous ORM for Python. Triggers allow you to automate database actions or perform additional tasks when certain events occur, such as inserting, updating, or deleting records.

## What are database triggers?

A database trigger is a stored procedure that is automatically executed in response to specific events or actions on a table. Triggers can be used to enforce business rules, perform calculations, update related tables, or log changes.

## Setting up Tortoise ORM

Before we dive into using triggers, let's make sure we have Tortoise ORM installed. You can install it using pip:

```
pip install tortoise-orm
```

## Creating a model with a trigger

To create a model with a trigger, we need to define the model class extending the `tortoise.models.Model` class, and use the `@tortoise.signals.post_save` decorator to specify the trigger function.

Here's an example of a `User` model with a trigger that updates the `last_modified` field whenever a user is updated:

```python
from tortoise import fields, models, Tortoise
from tortoise.signals import post_save


class User(models.Model):
    id = fields.IntField(pk=True)
    name = fields.CharField(50)
    last_modified = fields.DatetimeField(auto_now=True)

    async def trigger_update_last_modified(self, *args, **kwargs):
        self.last_modified = self.last_modified.now()

post_save.connect(User.trigger_update_last_modified, sender=User)
```

In this example, the `post_save` signal is triggered after saving a user model, which in turn calls the `trigger_update_last_modified` function to update the `last_modified` field to the current datetime.

## Handling triggers in database migrations

To ensure that the triggers are created or modified during database migrations, we need to define migration functions. Tortoise ORM provides a convenient decorator `@Tortoise.migrate` to handle the migration process.

Here's an example of a migration function that creates a trigger for the `User` model:

```python
from tortoise import Tortoise, fields


@Tortoise.migrate("users")
async def create_user_trigger():
    await Tortoise.get_connection().execute_script(
        """
        CREATE TRIGGER update_last_modified_trigger
        AFTER UPDATE ON users
        FOR EACH ROW
        EXECUTE FUNCTION update_last_modified();
        """
    )
```

In this example, the migration function executes a SQL script that creates the trigger `update_last_modified_trigger` for the `users` table. You can modify the script according to your specific trigger logic.

## Conclusion

Using database triggers with Tortoise ORM allows you to automate database actions and perform additional tasks effectively. By leveraging triggers, you can enforce business rules and maintain data integrity in your application. With Tortoise ORM's support for triggers and easy-to-use migration system, integrating triggers into your database workflow becomes even more seamless.

To explore more about Tortoise ORM, you can refer to the official documentation: [Tortoise ORM Documentation](https://tortoise-orm.readthedocs.io/)

Happy coding!