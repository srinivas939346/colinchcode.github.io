---
layout: post
title: "[python] Implementing auditing and versioning with Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Tortoise ORM is a powerful, easy-to-use asynchronous ORM (Object Relational Mapping) library for Python. It provides a simple and intuitive way to interact with databases, making it a popular choice for developing web applications.

One common requirement in many applications is the ability to audit and track changes to data, as well as keep a history of different versions of the data. In this article, we will explore how to implement auditing and versioning using Tortoise ORM.

## Table of Contents
- [Auditing](#auditing)
- [Versioning](#versioning)
- [Conclusion](#conclusion)

## Auditing

Auditing involves recording and tracking changes made to data. By implementing auditing, you can keep a log of who made the changes, when the changes were made, and what the changes were. This is useful for security and compliance purposes.

In Tortoise ORM, we can implement auditing using signals. Signals are an event-driven mechanism that allows us to perform certain actions before or after specific database operations.

To implement auditing, we need to define a model for our audit logs. This model will have fields to store information such as the user who made the changes, the timestamp of the changes, and the details of the changes.

Here's an example of how to define an audit log model using Tortoise ORM:

```python
from tortoise import fields, models

class AuditLog(models.Model):
    user = fields.CharField(max_length=255)
    timestamp = fields.DatetimeField(auto_now_add=True)
    details = fields.TextField()
```

Next, we can define a signal to handle the auditing before a database operation like saving or updating a model.

```python
from tortoise import signals

@signals.pre_save()
async def audit_log_handler(sender, instance, **kwargs):
    # Get the user information.
    user = get_current_user()  # Your implementation to get the current user.
    
    # Create an audit log entry.
    audit_log = AuditLog(user=user.username, details=instance.to_json())
    await audit_log.save()
```

In the above code, `pre_save()` is a signal decorator that will be called before saving an instance of any model. It calls the `audit_log_handler` function, which retrieves the current user and creates an `AuditLog` instance with details including the current state of the model.

By registering the signal handler, Tortoise ORM will automatically call the function before saving or updating any model data.

## Versioning

Versioning involves keeping a history of different versions of data. This can be useful to track changes over time and revert back to previous versions if needed.

To implement versioning with Tortoise ORM, we can create a separate model to store the different versions of a record. This model will have a foreign key to the original record, a timestamp, and the state of the record.

Here's an example of how to define a version model using Tortoise ORM:

```python
from tortoise import fields, models

class Version(models.Model):
    original_record = fields.ForeignKeyField("models.ModelName")
    timestamp = fields.DatetimeField(auto_now_add=True)
    state = fields.JSONField()
```

In the above code, `"models.ModelName"` should be replaced with the actual name of the model you want to version.

To create a new version whenever a record is updated, we can use the `pre_save()` signal in a similar way as before.

```python
@signals.pre_save()
async def versioning_handler(sender, instance, **kwargs):
    # Create a new version for the record.
    version = Version(original_record=instance, state=instance.to_json())
    await version.save()
```

Just like the auditing example, the `versioning_handler` function creates a new `Version` instance with the current state of the record and saves it.

With the above implementation, every time a record is saved or updated, a new version will be created and stored in the `Version` table.

## Conclusion

Auditing and versioning are important features in many applications to track and maintain data integrity. With Tortoise ORM, implementing auditing and versioning is straightforward using signals and separate models for audit logs and versions.

By following the examples provided in this article, you can easily incorporate auditing and versioning into your Tortoise ORM-based applications. Remember to customize the code snippets according to your specific requirements and models.

References:
- [Tortoise ORM Documentation](https://tortoise-orm.readthedocs.io/)
- [Django Signals](https://docs.djangoproject.com/en/3.2/topics/signals/)