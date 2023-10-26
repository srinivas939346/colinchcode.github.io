---
layout: post
title: "[python] Retrieving multiple records using Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Tortoise ORM is an easy-to-use, async ORM for Python that provides a simple interface to interact with databases. In this guide, we'll explore how to retrieve multiple records from a database table using Tortoise ORM.

### 1. Connecting to the database

Before we can retrieve records, we need to establish a connection to the database. Assuming you have already installed Tortoise ORM and have a database set up, here's an example of how you can connect to the database:

```python
from tortoise import Tortoise

async def connect_to_db():
    await Tortoise.init(
        db_url='postgres://user:password@localhost:5432/db_name',
        modules={'models': ['your_app.models']}
    )
    # Generate the schema
    await Tortoise.generate_schemas()

# Call the connect_to_db function
await connect_to_db()
```

Make sure to replace `user`, `password`, `localhost`, `5432`, and `db_name` with your own database credentials.

### 2. Defining the model

Next, let's define a model that corresponds to the table from which we want to retrieve records. Here's an example model class:

```python
from tortoise import fields, models

class Product(models.Model):
    id = fields.IntField(pk=True)
    name = fields.CharField(max_length=255)
    price = fields.DecimalField(max_digits=10, decimal_places=2)
```

### 3. Retrieving multiple records

To retrieve multiple records from the `Product` table, we can use the `all()` method provided by the Tortoise ORM. This method returns a queryset containing all the records in the table. Here's an example of how you can use it:

```python
products = await Product.all()
```

The `products` variable will now hold a list of `Product` objects representing the records retrieved from the database.

### 4. Filtering records

If you want to retrieve only a subset of the records that match certain criteria, you can use the `filter()` method. Here's an example that retrieves all products with a price greater than $50:

```python
products = await Product.filter(price__gt=50)
```

The `filter()` method accepts keyword arguments that define the filtering criteria. In this case, we use the `price__gt` argument to specify that the price should be greater than 50.

### 5. Further querying

Tortoise ORM provides a rich set of methods for querying and manipulating data. You can chain multiple query methods together to build complex queries. Here are a few examples:

- Sorting records: Use the `order_by()` method to sort the records based on a specific field.
- Limiting the number of records: Use the `limit()` method to retrieve only a certain number of records.
- Paginating records: Use the `offset()` and `limit()` methods together to retrieve records in batches.

For more information on querying with Tortoise ORM, refer to the [official documentation](https://tortoise-orm.readthedocs.io/).

That's it! You now know how to retrieve multiple records from a database table using Tortoise ORM. Experiment with different querying techniques to retrieve the data you need efficiently.