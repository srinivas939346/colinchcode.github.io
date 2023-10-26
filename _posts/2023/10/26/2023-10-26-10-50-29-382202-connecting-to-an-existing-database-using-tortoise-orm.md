---
layout: post
title: "[python] Connecting to an existing database using Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Tortoise ORM is an easy-to-use and powerful Object-Relational Mapping (ORM) tool for Python. It allows you to interact with databases using Python classes and objects. In this tutorial, we will see how to connect to an existing database using Tortoise ORM.

## Prerequisites

Before getting started, make sure you have the following prerequisites installed on your machine:

- Python (version 3.7 or higher)
- Tortoise ORM (install using `pip install tortoise-orm`)

## Connecting to the database

To connect to an existing database using Tortoise ORM, you need to define a connection configuration. This configuration provides the necessary details to establish a connection, such as the database type, host, port, username, password, and database name.

Here's an example of connecting to a PostgreSQL database:

```python
from tortoise import Tortoise

# Define the connection configuration
config = {
    'connections': {
        'default': {
            'engine': 'tortoise.backends.asyncpg',
            'credentials': {
                'host': 'localhost',
                'port': '5432',
                'user': 'your_username',
                'password': 'your_password',
                'database': 'your_database'
            }
        }
    },
    'apps': {
        'models': {
            'models': ['your_app.models'],
            'default_connection': 'default'
        }
    }
}

# Initialize Tortoise ORM
Tortoise.init(config)

# Start the event loop
Tortoise.run_async()
```

Replace the placeholder values (your_username, your_password, your_database, your_app.models) with your actual database credentials and your application's models.

Here, we are using the `tortoise.backends.asyncpg` engine for connecting to a PostgreSQL database. Make sure to install the appropriate database backend package accordingly.

## Closing the connection

Once you are done with your database operations, it's important to close the connection to release the resources. Here's how you can close the connection:

```python
# Close the connection
Tortoise.close_connections()
```

## Conclusion

Connecting to an existing database using Tortoise ORM is straightforward. By defining the connection configuration and initializing Tortoise ORM, you can start interacting with your database in a Pythonic way.

If you have any further questions or want to explore more about Tortoise ORM, check out the official [documentation](https://tortoise-orm.readthedocs.io/en/latest/) for detailed information.

Happy coding!