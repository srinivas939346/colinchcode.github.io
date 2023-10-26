---
layout: post
title: "[python] Integrating Tortoise ORM with other ORM libraries (e.g., SQLAlchemy)"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Tortoise ORM is a powerful asynchronous Object Relational Mapping (ORM) library for Python, which primarily supports database operations using the asyncio framework. However, there might be cases where you want to use Tortoise ORM alongside other ORM libraries like SQLAlchemy. This could be due to specific requirements of your project or the need to integrate with existing codebases. In this blog post, we will explore how to integrate Tortoise ORM with other ORM libraries effectively.

## Why integrate Tortoise ORM with other ORM libraries?

Integrating Tortoise ORM with other ORM libraries can offer several advantages. It allows you to leverage the unique features and capabilities of each library while maintaining compatibility with other parts of your codebase. Here are a few reasons why you might consider integrating Tortoise ORM with other ORM libraries:

1. Utilizing specific features: Different ORM libraries may offer different sets of features and functionalities. By integrating Tortoise ORM with another library like SQLAlchemy, you can take advantage of the specific features offered by each library, giving you more flexibility and options.

2. Migrating existing codebases: If you have an existing project that already uses another ORM library like SQLAlchemy, integrating Tortoise ORM can be a way to gradually transition your codebase to Tortoise ORM without having to rewrite everything from scratch.

3. Leveraging legacy databases: Some projects may be working with legacy databases that are already set up with a specific ORM library. Integrating Tortoise ORM with the existing library allows you to work with the legacy database without disrupting the existing code.

## Integrating Tortoise ORM with SQLAlchemy

To integrate Tortoise ORM with SQLAlchemy, we can make use of the `meta` feature provided by Tortoise ORM. The `meta` feature allows us to define entities based on SQLAlchemy models.

Here's an example code snippet that demonstrates how to integrate Tortoise ORM with SQLAlchemy:

```python
import sqlalchemy

# Define a SQLAlchemy model
Base = sqlalchemy.ext.declarative.declarative_base()

class User(Base):
    __tablename__ = 'users'
    id = sqlalchemy.Column(sqlalchemy.Integer, primary_key=True)
    name = sqlalchemy.Column(sqlalchemy.String)
    email = sqlalchemy.Column(sqlalchemy.String)

# Create the Tortoise ORM model
from tortoise import fields, models

class TortoiseUser(models.Model):
    id = fields.IntField(pk=True)
    name = fields.CharField(max_length=255)
    email = fields.CharField(max_length=255)

    class Meta:
        table = 'users' # Use the same table name as the SQLAlchemy model

# Get the SQLAlchemy connection
engine = sqlalchemy.create_engine('sqlite:///database.db')

# Create the Tortoise ORM connection
from tortoise import Tortoise
Tortoise.init_models(["path.to.your.models"], "models") # Specify the path to your Tortoise models

# Register the SQLAlchemy connection with Tortoise ORM
Tortoise.register_connection("default", **{
    "engine": "tortoise.backends.asyncpg",
    "credentials": {
        "host": "localhost",
        "port": "5432",
        "user": "user",
        "password": "password",
        "database": "database",
    }
})

# Run migrations with Tortoise ORM
Tortoise.generate_schemas()

# Query the database using both SQLAlchemy and Tortoise ORM
with engine.connect() as conn:
    sqlalchemy_users = conn.execute(sqlalchemy.select([User])).fetchall()
    tortoise_users = TortoiseUser.all()

    # Do something with the results
    for user in sqlalchemy_users:
        print(user.name)

    for user in tortoise_users:
        print(user.name)
```

In the code snippet above, we define a SQLAlchemy model `User` and a Tortoise ORM model `TortoiseUser`. We create a SQLAlchemy connection using `create_engine` and a Tortoise ORM connection using `Tortoise.register_connection`.

By leveraging both SQLAlchemy and Tortoise ORM, we can query the database using the respective ORM libraries and work with the results interchangeably.

## Conclusion

Integrating Tortoise ORM with other ORM libraries like SQLAlchemy can offer a range of benefits, from leveraging specific features to migrating existing codebases. By using the `meta` feature provided by Tortoise ORM, you can easily integrate Tortoise ORM with other ORM libraries and take advantage of their unique capabilities.

Keep in mind that while integrating different ORM libraries can be beneficial, it could also add complexity to your codebase. Therefore, it's important to evaluate the trade-offs and carefully plan the integration based on the specific requirements of your project.

References:
- [Tortoise ORM documentation](https://tortoise-orm.readthedocs.io/)
- [SQLAlchemy documentation](https://docs.sqlalchemy.org/)