---
layout: post
title: "[python] Using schema introspection in Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Tortoise ORM is a Python library that provides an easy-to-use interface for working with databases. One of the useful features it offers is schema introspection, which allows you to retrieve information about the database schema directly from the database itself.

## What is schema introspection?

Schema introspection is the process of examining the structure and metadata of a database schema. It allows you to retrieve information about tables, columns, and relationships without having to manually define them in your code.

## How to use schema introspection in Tortoise ORM

To use schema introspection in Tortoise ORM, you can use the `generate_schemas` function. This function takes a connection string as an argument and generates the necessary code to reflect the database schema.

```python
from tortoise import Tortoise, generate_schemas

async def introspect_schema(connection_string):
    await Tortoise.init(db_url=connection_string)
    await generate_schemas()

connection_string = "sqlite://db.sqlite3"
await introspect_schema(connection_string)
```

In the example above, we initialize Tortoise ORM with the provided connection string and then call the `generate_schemas` function. This will generate the necessary code for the defined models to match the database schema.

## Retrieving information about the schema

Once the schema introspection is done, you can access the retrieved schema information through `Tortoise_ORM_DB_Client.connection.schema`. This returns a `Schema` instance, which provides methods to access the tables, columns, and relationships of the database schema.

```python
from tortoise import Tortoise, generate_schemas

async def introspect_schema(connection_string):
    await Tortoise.init(db_url=connection_string)
    await generate_schemas()

    schema = Tortoise.get_connection().schema
    tables = schema.get_tables()

    for table_name, table in tables.items():
        print(f"Table: {table_name}")
        for column in table.columns:
            print(f"- Column: {column.name}, type: {column.column_type}")

connection_string = "sqlite://db.sqlite3"
await introspect_schema(connection_string)
```

In the example above, we retrieve the schema object from the connection and then iterate over the tables. For each table, we print out the table name and the information about its columns.

## Conclusion

Schema introspection in Tortoise ORM provides a convenient way to retrieve information about the database schema without the need to manually define it in your code. By using the `generate_schemas` function and accessing the `Schema` object, you can easily retrieve information about tables, columns, and relationships. This can be particularly useful when working with existing databases or when you need to dynamically interact with the database schema.