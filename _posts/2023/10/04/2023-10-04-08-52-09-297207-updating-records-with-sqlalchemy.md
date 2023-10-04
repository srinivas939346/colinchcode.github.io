---
layout: post
title: "[python] Updating Records with SQLAlchemy"
description: " "
date: 2023-10-04
tags: [python]
comments: true
share: true
---

When working with databases, it is often necessary to update existing records. In this article, we will explore how to update records using SQLAlchemy, a powerful and flexible Object-Relational Mapping (ORM) library for Python.

## Prerequisites

To follow along with this tutorial, you need to have the following software installed on your machine:

- Python (version 3 or later)
- SQLAlchemy

You can install SQLAlchemy by running the following command:

```shell
pip install sqlalchemy
```

## Connecting to the Database

Before we can update records, we need to establish a connection to the database. For this example, let's assume we have a SQLite database file named `example.db`. We can connect to the database using the following code:

```python
from sqlalchemy import create_engine

engine = create_engine('sqlite:///example.db')
```

## Defining the Table

Next, we need to define the table we want to update. We can do this using SQLAlchemy's `Table` class. Here's an example of defining a `users` table with two columns - `id` and `name`:

```python
from sqlalchemy import MetaData, Table, Column, Integer, String

metadata = MetaData()

users = Table(
    'users',
    metadata,
    Column('id', Integer, primary_key=True),
    Column('name', String)
)
```

## Updating Records

Now that we have connected to the database and defined the table, we can update records.

To update a record in SQLAlchemy, we need to use the `update` function. The `update` function takes two arguments - the table we want to update and the values we want to set.

Here's an example of updating a user with a specific ID:

```python
from sqlalchemy import update

with engine.connect() as conn:
    update_query = (
        update(users)
        .where(users.c.id == 1)
        .values(name="John Doe")
    )
    conn.execute(update_query)
```

In this example, we update the `name` column of the user with ID 1 to "John Doe".

## Updating Multiple Records

To update multiple records at once, we can use additional conditions in the `where` clause. Here's an example of updating all the users with the name "John" to "John Doe":

```python
from sqlalchemy import update

with engine.connect() as conn:
    update_query = (
        update(users)
        .where(users.c.name == "John")
        .values(name="John Doe")
    )
    conn.execute(update_query)
```

This will update all the users with the name "John" to "John Doe".

## Conclusion

In this article, we learned how to update records using SQLAlchemy. We covered how to connect to the database, define a table, and perform updates on single and multiple records. SQLAlchemy provides a powerful and intuitive way to interact with databases, making it easy to work with and manipulate data. Happy coding!

**References:**

- [SQLAlchemy Documentation](https://docs.sqlalchemy.org/)
- [SQLAlchemy Tutorial](https://www.tutorialspoint.com/sqlalchemy/index.htm)