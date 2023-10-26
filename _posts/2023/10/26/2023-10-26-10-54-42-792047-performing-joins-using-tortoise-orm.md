---
layout: post
title: "[python] Performing joins using Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When working with databases, it is common to need to query data from multiple tables and combine the results using joins. Tortoise ORM, a Python asynchronous ORM, provides a convenient way to perform joins and retrieve related data from multiple tables.

In this blog post, we will explore how to perform joins using Tortoise ORM and demonstrate it with a practical example.

## Table of Contents
- [Introduction](#introduction)
- [Performing Inner Joins](#performing-inner-joins)
- [Performing Outer Joins](#performing-outer-joins)
- [Conclusion](#conclusion)

## Introduction
Tortoise ORM is an easy-to-use ORM that supports multiple database backends and provides a high-level API to perform database operations. It makes it simple to work with relational databases and handle complex data relationships.

## Performing Inner Joins
An inner join combines rows from two or more tables based on a related column between them. To perform an inner join using Tortoise ORM, we can use the `prefetch_related()` method along with the `join()` method.

```python
from tortoise.query_utils import Prefetch
from models import User, Post

async def get_users_with_posts():
    users = await User.all().prefetch_related(
        Prefetch('posts', queryset=Post.all())
    )

    for user in users:
        for post in user.posts:
            print(f"User: {user.name}, Post: {post.title}")

# Usage
await get_users_with_posts()
```

In the example above, we have two models: `User` and `Post`. We use the `prefetch_related()` method to fetch the related posts for each user using the `posts` field. Then, we iterate over the users and their posts to print the output.

## Performing Outer Joins
An outer join retrieves all rows from one table and the matching rows from another table. Tortoise ORM supports performing outer joins using the `prefetch_related()` method along with the `join()` method.

```python
from tortoise.query_utils import Prefetch
from models import User, Comment

async def get_users_with_comments():
    users = await User.all().prefetch_related(
        Prefetch('comments', queryset=Comment.all().join(User))
    )

    for user in users:
        for comment in user.comments:
            print(f"User: {user.name}, Comment: {comment.text}")

# Usage
await get_users_with_comments()
```

In the example above, we have two models: `User` and `Comment`. We use the `prefetch_related()` method to fetch the related comments for each user using the `comments` field. We perform an outer join between the `User` and `Comment` models using the `join()` method. Then, we iterate over the users and their comments to print the output.

## Conclusion
Performing joins in relational databases is a crucial aspect of retrieving and combining data from multiple tables. Tortoise ORM provides a simple and intuitive way to perform inner and outer joins using the `prefetch_related()` and `join()` methods. It allows you to work with complex data relationships easily and efficiently.

To learn more about Tortoise ORM and its capabilities, refer to the official documentation: [Tortoise ORM Documentation](https://tortoise-orm.readthedocs.io/)

Happy coding!