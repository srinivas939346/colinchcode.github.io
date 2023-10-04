---
layout: post
title: "[python] Lazy Loading in SQLAlchemy"
description: " "
date: 2023-10-04
tags: [python]
comments: true
share: true
---

Lazy loading is a technique used in SQLAlchemy to optimize database queries by deferring the loading of related objects until they are actually accessed. This helps to improve the performance of our application by reducing the number of database queries.

In SQLAlchemy, lazy loading is achieved through the use of **relationships**. Relationships define the association between two tables and allow us to specify how related objects should be loaded.

## How Lazy Loading Works

When we define a relationship between two tables in SQLAlchemy, by default, it is lazily loaded. This means that when we access a related object, SQLAlchemy will automatically execute a separate database query to fetch the related data.

For example, let's consider a `User` model that has a one-to-many relationship with a `Post` model. Each user can have multiple posts. When we query a user from the database, SQLAlchemy will not load the associated posts immediately. Instead, it will load them only when we actually try to access the `posts` attribute of the user object.

## Enabling Lazy Loading

Lazy loading is the default behavior in SQLAlchemy, so there's no need to explicitly enable it. However, we can configure the lazy loading behavior by specifying different options when defining the relationship.

The `lazy` parameter can be used to control the loading strategy. Here are some common options:

- `select` (default): Loads the related objects using a separate SELECT statement when accessed.
- `joined`: Performs a JOIN between the two tables to load the related objects in the initial query.
- `subquery`: Uses a subquery to load the related objects.
- `noload`: Disables lazy loading altogether. The related objects are never loaded automatically.

```python
from sqlalchemy import Column, Integer, String, ForeignKey
from sqlalchemy.orm import relationship

class User(Base):
    __tablename__ = 'users'

    id = Column(Integer, primary_key=True)
    name = Column(String)
    posts = relationship('Post', lazy='select')

class Post(Base):
    __tablename__ = 'posts'

    id = Column(Integer, primary_key=True)
    title = Column(String)
    user_id = Column(Integer, ForeignKey('users.id'))
```

In the above example, we have specified the `lazy` option as `'select'` for the `posts` relationship of the `User` model. This means that when we access the `posts` attribute of a user, SQLAlchemy will execute a separate SELECT statement to retrieve the related posts.

## Eager Loading

In some cases, it might be more efficient to load all related objects upfront instead of making individual queries for each object. This can be achieved using eager loading.

To enable eager loading, we can pass the `joinedload` option to the query. SQLAlchemy will then perform a join query to load all related objects in a single query.

```python
from sqlalchemy.orm import joinedload

user = session.query(User).options(joinedload(User.posts)).filter(User.id == 1).first()
```

In the above example, we use the `options` method to specify the `joinedload` option for the `User.posts` relationship. Now, when we query a user, all associated posts will be loaded in a single query.

## Conclusion

Lazy loading is a powerful technique in SQLAlchemy that helps optimize database queries by deferring the loading of related objects until they are actually accessed. By properly configuring the lazy loading behavior, we can improve the performance of our application and reduce unnecessary database queries. Eager loading can also be used in certain scenarios to load all related objects upfront in a single query.