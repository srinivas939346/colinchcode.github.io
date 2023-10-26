---
layout: post
title: "[python] Aggregations and annotations in Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Tortoise ORM is a powerful and easy-to-use Object-Relational Mapping (ORM) library for Python that simplifies database interactions. In addition to basic CRUD operations, Tortoise ORM provides advanced features like aggregations and annotations, which allow you to perform complex computations and aggregate data.

### Aggregations

Aggregations in Tortoise ORM allow you to calculate aggregate values from a set of records. You can perform various types of aggregations, such as counting, summing, averaging, and finding the maximum or minimum value.

To perform an aggregation, you need to use the `annotate()` method on a queryset. Here's an example that demonstrates how to get the count of all records in a table:

```python
from tortoise import Tortoise, fields, run_async
from tortoise.models import Model


class Book(Model):
    name = fields.CharField(max_length=255)

async def main():
    await Tortoise.init(db_url='sqlite://:memory:', modules={'models': ['__main__']})

    count = await Book.annotate(count=models.Count('*')).all().values('count').first()

    print(count)

    await Tortoise.close_connections()

run_async(main())
```

In this example, the `annotate()` method is used to add an aggregation field called `count` to the queryset. The [`models.Count`](https://tortoise-orm.readthedocs.io/en/latest/aggregations.html#count) function is used for counting all records. The result is obtained by calling `all().values('count').first()`, which fetches the first record in the queryset and retrieves its `count` value.

### Annotations

Annotations, on the other hand, allow you to add additional computed fields to the queryset. These computed fields are not derived from the database columns but are instead calculated using expressions, functions, or even other annotations.

Here's an example that demonstrates how to use annotations in Tortoise ORM:

```python
from tortoise import Tortoise, fields, run_async
from tortoise.models import Model


class Book(Model):
    name = fields.CharField(max_length=255)
    price = fields.DecimalField(max_digits=5, decimal_places=2)

async def main():
    await Tortoise.init(db_url='sqlite://:memory:', modules={'models': ['__main__']})

    annotated_books = await Book.annotate(discounted_price=models.F('price') * 0.8).all().values()

    print(annotated_books)

    await Tortoise.close_connections()

run_async(main())
```

In this example, we define a computed field called `discounted_price` using the `annotate()` method. This field is calculated by multiplying the `price` field with a discount factor of 0.8. The `values()` method is used to retrieve all records with their annotated fields.

Both aggregations and annotations provide powerful ways to manipulate and compute data in Tortoise ORM. They can be used to generate reports, perform statistical analysis, or create custom data transformations. By leveraging these features, you can make your database interactions more efficient and flexible.