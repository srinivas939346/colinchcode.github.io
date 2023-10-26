---
layout: post
title: "[python] Using raw SQL queries with Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In some cases, you may find it necessary to execute raw SQL queries with Tortoise ORM, a Python asyncio ORM framework. Raw SQL queries allow you to write custom complex queries that go beyond the capabilities of the ORM.

Here's how you can use raw SQL queries with Tortoise ORM.

## Executing Raw Queries
To execute raw SQL queries using Tortoise ORM, you can use the `db.execute_query()` method. This method allows you to execute any arbitrary SQL query.

First, import the necessary modules:
```python
from tortoise import Tortoise
from tortoise.backends.asyncpg import AsyncpgDBClient
```

Next, configure the Tortoise ORM to use the desired database:
```python
Tortoise.init(config={
    "connections": {"default": "postgres://user:password@localhost:5432/db_name"},
    "apps": {
        "models": {
            "models": ["path.to.models"],
            "default_connection": "default",
        }
    },
})
```

Now, you can execute raw queries using `db.execute_query()`:
```python
db_client = Tortoise.get_connection("default")
result = await db_client.execute_query("SELECT * FROM users;")
```

The `execute_query()` method returns the result of the query as a list of dictionaries, where each dictionary represents a row. You can use this result to process your query's output as needed.

## Executing Raw Queries with Parameters
You can also pass parameters to your raw SQL queries in order to prevent SQL injection attacks. To do this, pass the parameters as a separate argument to the `execute_query()` method.

Here's an example:
```python
age = 25
result = await db_client.execute_query("SELECT * FROM users WHERE age > $1;", age)
```

In this example, the `age` variable is passed as a parameter to the query, reducing the risk of SQL injection.

Remember to always use parameterized queries whenever you're working with user input or any dynamic data.

## Conclusion
Using raw SQL queries with Tortoise ORM can be a powerful tool when dealing with complex or specialized queries that cannot be easily expressed using the ORM's query API. Just be cautious when working with raw queries to ensure proper handling of user input and prevent SQL injection attacks.