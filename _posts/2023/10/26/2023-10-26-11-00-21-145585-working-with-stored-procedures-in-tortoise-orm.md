---
layout: post
title: "[python] Working with stored procedures in Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When working with databases, there are times when you might need to execute stored procedures to perform certain tasks or data manipulations. Tortoise ORM, a Python library for asynchronous ORM, provides a convenient way to work with stored procedures.

In this blog post, we will explore how to use Tortoise ORM to execute stored procedures in a Python application.

## Table of Contents

- [Introduction to stored procedures](#introduction-to-stored-procedures)
- [Setting up Tortoise ORM](#setting-up-tortoise-orm)
- [Executing a simple stored procedure](#executing-a-simple-stored-procedure)
- [Passing parameters to a stored procedure](#passing-parameters-to-a-stored-procedure)
- [Retrieving results from a stored procedure](#retrieving-results-from-a-stored-procedure)
- [Conclusion](#conclusion)
- [References](#references)

## Introduction to stored procedures

Stored procedures are pre-compiled SQL code blocks that are stored on the database server and can be executed when needed. They provide a way to encapsulate a series of SQL statements into a single entity that can be easily called from an application.

Stored procedures offer many advantages, including improved performance, enhanced security, and better code organization.

## Setting up Tortoise ORM

To get started with Tortoise ORM, you need to install it using pip:

```python
pip install tortoise-orm
```

You will also need to have a database server set up and configure the connection details in your application. Tortoise ORM supports various databases like SQLite, MySQL, PostgreSQL, and others.

## Executing a simple stored procedure

Let's start by creating a simple stored procedure that inserts a new record into a table. Assuming you have a `users` table, the following stored procedure inserts a new user record:

```sql
CREATE PROCEDURE `insert_user` (IN name VARCHAR(255), IN email VARCHAR(255))
BEGIN
    INSERT INTO users (name, email) VALUES (name, email);
END
```

To execute this stored procedure using Tortoise ORM, you can use the `execute_query` method:

```python
from tortoise import Tortoise

async def insert_user(name: str, email: str):
    await Tortoise.init(db_url='sqlite://:memory:', modules={'models': ['app.models']})
    await Tortoise.generate_schemas()

    await Tortoise.execute_query(
        "CALL insert_user(:name, :email)",
        {'name': name, 'email': email}
    )

    await Tortoise.close_connections()
```

In the example above, we initialize Tortoise ORM, generate the database schema, execute the stored procedure using `execute_query`, and then close the connections. Replace `'app.models'` with the appropriate module that defines your models.

## Passing parameters to a stored procedure

Stored procedures often require parameters for their execution. Tortoise ORM allows you to pass parameters to a stored procedure using named placeholders in the SQL query.

Let's update our `insert_user` stored procedure to accept a password parameter:

```sql
CREATE PROCEDURE `insert_user` (IN name VARCHAR(255), IN email VARCHAR(255), IN password VARCHAR(255))
BEGIN
    INSERT INTO users (name, email, password) VALUES (name, email, password);
END
```

To execute this stored procedure with a password parameter, you can modify the `execute_query` method:

```python
await Tortoise.execute_query(
    "CALL insert_user(:name, :email, :password)",
    {'name': name, 'email': email, 'password': password}
)
```

## Retrieving results from a stored procedure

Stored procedures can also return results, such as querying data from the database. Tortoise ORM provides the `fetch_one_query` and `fetch_all_query` methods to retrieve results from a stored procedure.

Let's create a stored procedure that returns all users with a specific role:

```sql
CREATE PROCEDURE `get_users_by_role` (IN role VARCHAR(255))
BEGIN
    SELECT * FROM users WHERE role = role;
END
```

To retrieve the users with a specific role, you can use the `fetch_all_query` method:

```python
results = await Tortoise.fetch_all_query(
    "CALL get_users_by_role(:role)",
    {'role': 'admin'}
)

for user in results:
    print(user.name, user.email)
```

In the example above, we execute the stored procedure and iterate over the results to print the name and email of each user.

## Conclusion

Working with stored procedures in Tortoise ORM allows you to leverage the power and efficiency of SQL code on your database server while still using an elegant and Pythonic ORM in your application. You can execute stored procedures, pass parameters, and retrieve results easily.

In this blog post, we covered the basics of working with stored procedures in Tortoise ORM. Make sure to refer to the official documentation for more advanced operations and features.

## References

- [Tortoise ORM documentation](https://tortoise-orm.readthedocs.io)
- [MySQL stored procedures documentation](https://dev.mysql.com/doc/refman/8.0/en/stored-routines.html)