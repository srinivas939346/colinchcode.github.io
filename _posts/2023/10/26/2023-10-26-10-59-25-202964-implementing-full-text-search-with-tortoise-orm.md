---
layout: post
title: "[python] Implementing full-text search with Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When building applications that involve searching through large amounts of text data, implementing full-text search functionality is often necessary. This allows users to find relevant information quickly and efficiently. In this blog post, we will explore how to implement full-text search using Tortoise ORM, a powerful ORM (Object-Relational Mapping) tool for Python.

**Table of Contents**
- [What is Full-Text Search?](#what-is-full-text-search)
- [Setting up Tortoise ORM](#setting-up-tortoise-orm)
- [Implementing Full-Text Search](#implementing-full-text-search)
- [Conclusion](#conclusion)

## What is Full-Text Search?

Full-text search is the process of searching for keywords or phrases in a collection of text documents. Unlike traditional database queries, which rely on exact matches, full-text search allows for more flexible and intuitive searching by considering the relevance and proximity of words within the text.

## Setting up Tortoise ORM

First, we need to install Tortoise ORM using pip:

```python
pip install tortoise-orm
```

Next, let's create a connection to our database using Tortoise ORM:

```python
from tortoise import Tortoise

TORTOISE_ORM = {
    "connections": {
        "default": {
            "engine": "tortoise.backends.asyncpg",
            "credentials": {
                "host": "localhost",
                "user": "username",
                "password": "password",
                "database": "mydatabase",
            },
        },
    },
    "apps": {
        "models": {
            "models": ["path.to.models"],
            "default_connection": "default",
        },
    },
}

async def setup_db():
    await Tortoise.init(TORTOISE_ORM)
    await Tortoise.generate_schemas()

async def close_db():
    await Tortoise.close_connections()
```

Ensure you replace `"localhost"`, `"username"`, `"password"`, and `"mydatabase"` with the appropriate values for your database configuration.

## Implementing Full-Text Search

To implement full-text search with Tortoise ORM, we'll make use of the `MATCH` operator, which allows us to specify the columns we want to search against and the search terms we are looking for.

Let's assume we have a `BlogPost` model with a `title` and `content` field. We can perform a full-text search on these fields using the following code:

```python
from tortoise.models import Model
from tortoise import fields

class BlogPost(Model):
    id = fields.IntField(pk=True)
    title = fields.CharField(max_length=255)
    content = fields.TextField()

    class Meta:
        table = "blog_post"

async def search_posts(query: str):
    posts = await BlogPost.filter(
        fields__matches=query
    ).order_by("-id").all()

    for post in posts:
        print(post.title)
```

In this example, we use the `filter()` method to specify the full-text search query. The `fields__matches` filter maps to the `MATCH` operator, which performs the actual search on the specified fields. We then order the results by `id` in descending order using `order_by()`.

## Conclusion

Implementing full-text search using Tortoise ORM is a straightforward process that allows us to easily incorporate powerful search functionality into our Python applications. By leveraging the `MATCH` operator, we can search through text data efficiently and provide users with relevant results.

[Tortoise ORM Documentation](https://tortoise-orm.readthedocs.io/)

[Full-Text Search in PostgreSQL](https://www.postgresql.org/docs/13/textsearch.html)