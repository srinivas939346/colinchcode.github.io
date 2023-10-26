---
layout: post
title: "[python] Handling concurrent access with Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When building applications that handle concurrent access to a database, it's essential to ensure data integrity and prevent conflicts. Tortoise ORM, a Python library, offers several mechanisms for handling concurrent access efficiently.

## Optimistic Concurrency Control (OCC)

One common approach to handling concurrent access is through **Optimistic Concurrency Control**. It works by assuming that conflicts are rare and that multiple transactions can operate independently most of the time. Here's how you can implement OCC with Tortoise ORM:

1. Start by defining a `version` field in your model that will keep track of the object's version.
   
   ```python
   from tortoise import fields, Model

   class MyModel(Model):
       version = fields.IntField()
       # Other fields...
   ```
   
2. Whenever a transaction wants to update a record, it retrieves the current version and increments it.
   
   ```python
   async def update_record(model_id, new_data):
       model = await MyModel.get(id=model_id)
       model.version += 1
       model.save()
   ```

3. When committing a transaction, Tortoise ORM automatically adds a `WHERE` clause to the update statement, verifying that the stored `version` matches the expected value.
   
   ```python
   await update_record(model_id, new_data)
   ```

   The generated SQL update statement includes: `AND version = <expected_value>`. If the version has changed since the transaction started, the query will not update any rows, and you can handle the conflict accordingly.

## Pessimistic Concurrency Control (PCC)

Another approach is **Pessimistic Concurrency Control**, which locks the data during the transaction to prevent conflicts. Tortoise ORM allows you to use database locks to implement PCC.

1. Start a transaction and acquire a lock on the rows you want to modify.
   
   ```python
   async def update_record(model_id, new_data):
       async with db.transaction():
           async with db.lock_table("my_model") as lock:
               model = await MyModel.get(id=model_id)
               # Update the record
               model.save()
   ```

2. While a transaction holds the lock, other transactions trying to access the same rows will be blocked until the lock is released.

   ```python
   await update_record(model_id, new_data)
   ```

   PCC ensures that only one transaction can modify the locked data at a time, avoiding conflicts.

## Conclusion

Handling concurrent access is a crucial consideration when working with databases. Both Optimistic Concurrency Control (OCC) and Pessimistic Concurrency Control (PCC) are effective strategies for managing conflicts. Tortoise ORM provides support for both approaches, allowing you to choose the one that best fits your application's requirements.

To learn more about Tortoise ORM and its concurrency control mechanisms, refer to the [official documentation](https://tortoise-orm.readthedocs.io/).