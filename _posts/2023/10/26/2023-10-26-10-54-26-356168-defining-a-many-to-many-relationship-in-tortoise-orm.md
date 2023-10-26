---
layout: post
title: "[python] Defining a many-to-many relationship in Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In this blog post, we will focus on how to define a many-to-many relationship using Tortoise ORM. A many-to-many relationship occurs when one entity can be associated with multiple instances of another entity, and vice versa.

Let's take an example scenario where we have two models - `User` and `Role`. Each user can have multiple roles, and each role can be assigned to multiple users.

To define this many-to-many relationship in Tortoise ORM, we need to create an intermediate table that holds the associations between users and roles. This table is commonly referred to as a "through" table.

First, let's define our models:

```python
from tortoise import fields
from tortoise.models import Model


class User(Model):
    id = fields.IntField(pk=True)
    name = fields.CharField(max_length=255)
    roles = fields.ManyToManyField(
        "models.Role", related_name="users", through="user_role"
    )


class Role(Model):
    id = fields.IntField(pk=True)
    name = fields.CharField(max_length=255)
    users = fields.ManyToManyField(
        "models.User", related_name="roles", through="user_role"
    )
```

In the `User` model, we define a `roles` field as a `ManyToManyField` with related name set to "users". We also specify the `through` parameter as "user_role", which is the name of the intermediate table.

Similarly, in the `Role` model, we define a `users` field as a `ManyToManyField` with related name set to "roles". The `through` parameter is again set to "user_role".

Now, let's create the through table:

```python
class UserRole(Model):
    user = fields.ForeignKeyField("models.User", related_name="user_roles")
    role = fields.ForeignKeyField("models.Role", related_name="role_users")
```

We define two foreign key fields - `user` and `role` - in the `UserRole` model to reference the `User` and `Role` models, respectively. We also specify the related names to access the associations from both ends.

That's it! We have successfully defined the many-to-many relationship using Tortoise ORM. We can now use these models to query and manipulate data.

Here's an example of how to create a user with roles:

```python
async def create_user_with_roles():
    user = await User.create(name="John")
    role1 = await Role.create(name="Admin")
    role2 = await Role.create(name="User")
    await user.roles.add(role1, role2)

    # Access associated roles
    user_roles = await user.roles.all()
    for role in user_roles:
        print(role.name)  # Output: Admin, User
```

In this example, we create a user named "John" and two roles - "Admin" and "User". Then, using the `add` method, we associate the roles with the user.

To access the associated roles, we can use the `roles` attribute on the user model and call the `all` method, which returns a queryset of related roles.

That's a brief overview of how to define a many-to-many relationship in Tortoise ORM. With its intuitive syntax and powerful features, Tortoise ORM makes working with databases and managing relationships a breeze.

References:
- Tortoise ORM documentation: [https://tortoise-orm.readthedocs.io](https://tortoise-orm.readthedocs.io)
- Tortoise ORM GitHub repository: [https://github.com/tortoise/tortoise-orm](https://github.com/tortoise/tortoise-orm)