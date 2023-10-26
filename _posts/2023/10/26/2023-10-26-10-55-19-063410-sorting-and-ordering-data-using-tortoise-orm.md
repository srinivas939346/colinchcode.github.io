---
layout: post
title: "[python] Sorting and ordering data using Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Tortoise ORM is an easy-to-use asynchronous database toolkit for Python. It provides a simple and intuitive way to interact with relational databases asynchronously. In this blog post, we'll explore how to sort and order data using Tortoise ORM.

## Table of Contents
1. [Sorting Data](#sorting-data)
2. [Ordering Data](#ordering-data)
3. [Combining Sorting and Ordering](#combining-sorting-and-ordering)
4. [Conclusion](#conclusion)

## Sorting Data<a name="sorting-data"></a>

To sort data in Tortoise ORM, you can use the `order_by` method provided by the queryset. The `order_by` method accepts one or more field names as arguments and sorts the query results based on those field values.

Let's assume we have a `User` model with fields `id`, `name`, and `age`. To retrieve the users sorted by their name in ascending order, we can use the following code:

```python
from tortoise.models import Model
from tortoise import fields

class User(Model):
    id = fields.IntField(pk=True)
    name = fields.CharField(max_length=255)
    age = fields.IntField()

async def get_users_sorted_by_name():
    users = await User.all().order_by('name').values()
    return users
```

The `order_by` method is called on the `User` queryset, specifying the field `name` for sorting. The `values` method returns the queryset as a list of dictionaries representing the user objects.

## Ordering Data<a name="ordering-data"></a>

Tortoise ORM also allows you to order the data in descending order by prefixing the field name with a minus "-" sign. Let's update our previous example to retrieve users ordered by their age in descending order:

```python
async def get_users_ordered_by_age():
    users = await User.all().order_by('-age').values()
    return users
```

The `-age` argument in the `order_by` method sorts the users by their age in descending order.

## Combining Sorting and Ordering<a name="combining-sorting-and-ordering"></a>

You can also combine sorting and ordering to get more precise results. For example, if you want to retrieve users sorted by their age in descending order and then sort them by name in ascending order, you can use:

```python
async def get_users_sorted_and_ordered():
    users = await User.all().order_by('-age', 'name').values()
    return users
```

In the above example, the `order_by` method is called with two arguments, `-age` and `name`. This sorts the users by age in descending order and, if two users have the same age, then further sorts them by name in ascending order.

## Conclusion<a name="conclusion"></a>

Sorting and ordering data is essential when dealing with large datasets, and Tortoise ORM provides a convenient way to accomplish this. In this blog post, we've explored how to sort and order data using Tortoise ORM. With these techniques, you can easily customize the order in which your data is retrieved from the database.

Keep in mind that accurate sorting and ordering can have an impact on performance, especially with large datasets. It's always a good practice to analyze and optimize your queries accordingly.

To learn more about Tortoise ORM, you can refer to their official documentation: [Tortoise ORM Documentation](https://tortoise-orm.readthedocs.io/)