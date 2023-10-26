---
layout: post
title: "[python] Creating a new database using Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Tortoise ORM is a powerful Object-Relational Mapping library for Python that allows you to interact with databases using asynchronous programming. In this tutorial, we will learn how to create a new database using Tortoise ORM.

## Prerequisites

Make sure you have Tortoise ORM installed in your Python environment. You can install it using pip:

```python
pip install tortoise-orm
```

## Creating a database connection

To create a new database using Tortoise ORM, you first need to establish a connection to the database. Tortoise ORM supports various databases such as SQLite, MySQL, and PostgreSQL.

Here's an example of how to create a connection to a SQLite database:

```python
from tortoise import Tortoise

# Initialize the connection
Tortoise.init(db_url='sqlite://db.sqlite3', modules={'models': ['your_module.models']})

# Create the connection
Tortoise._connections['default'] = await Tortoise.get_connection('default')
```

Replace `'your_module.models'` with the module where your models are defined.

## Creating the database

Once the connection is established, you can create the database by calling the `Tortoise.generate_schemas()` method. This method creates the necessary tables and indexes based on your model definitions.

```python
# Generate the schema
await Tortoise.generate_schemas()

# Close the connection
await Tortoise.close_connections()
```

Make sure to close the connection after generating the schema.

## Running the code

Save the above code in a Python file and execute it to create the database. You should see the database file generated in the specified location.

## Conclusion

Creating a new database using Tortoise ORM is fairly straightforward. By following the steps outlined in this tutorial, you can easily create a new database and start interacting with it using Tortoise ORM.

For more information on Tortoise ORM and its advanced features, check out the official documentation at [https://tortoise-orm.readthedocs.io](https://tortoise-orm.readthedocs.io).

Happy coding!