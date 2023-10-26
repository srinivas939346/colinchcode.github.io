---
layout: post
title: "[python] Inserting data into a table using Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Tortoise ORM is a lightweight async ORM for Python that provides an easy way to interact with databases. In this tutorial, we will learn how to insert data into a table using Tortoise ORM.

## Prerequisites
To follow along with this tutorial, you need to have Tortoise ORM installed. You can install it using pip:
```python
pip install tortoise-orm
```

## Creating the Model
Before we insert data into a table, we need to define a model that represents the table's structure. Let's say we want to insert data into a "users" table with three fields: "id" (integer), "name" (string), and "age" (integer). We can define the model as follows:

```python
from tortoise import fields
from tortoise.models import Model

class User(Model):
    id = fields.IntField(pk=True)
    name = fields.CharField(max_length=100)
    age = fields.IntField()
```

## Connecting to the Database
Next, we need to connect to the database. In this example, we will assume we are using SQLite as the database. You will need to provide the database URL specific to your configuration. 

```python
from tortoise import Tortoise

# Connect to the database
async def connect():
    await Tortoise.init(db_url='sqlite://users.db', modules={'models': ['your_module_name.models']})
    # Generate the schema
    await Tortoise.generate_schemas()

# Run the connect function
asyncio.run(connect())
```

## Inserting Data
Once we have the model defined and the database connected, we can insert data into the "users" table. To insert data, we create an instance of the model, set its fields, and then call the `save()` method.

```python
# Create a new user instance
user = User(name='John Doe', age=25)

# Save the user to the database
await user.save()
```

Alternatively, we can use the `.create()` method to create a new instance of the model and insert it into the database in one step.

```python
# Create and insert a new user
await User.create(name='Jane Smith', age=30)
```

## Closing the Connection
After we have finished inserting data, it is good practice to close the database connection. We can do this by calling the `Tortoise.close_connections()` method.

```python
# Close the database connection
await Tortoise.close_connections()
```

## Conclusion
In this tutorial, we have learned how to insert data into a table using Tortoise ORM. We defined a model to represent the table's structure and connected to the database. We then inserted data into the table using the model's `save()` and `create()` methods. Finally, we closed the database connection. Tortoise ORM provides an easy and intuitive way to interact with databases in Python.