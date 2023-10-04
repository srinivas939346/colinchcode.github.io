---
layout: post
title: "[python] Filtering and Querying Data with SQLAlchemy"
description: " "
date: 2023-10-04
tags: [python]
comments: true
share: true
---

SQLAlchemy is a popular Object-Relational Mapping (ORM) library for Python. It provides a high-level interface for working with databases, allowing developers to interact with the database in a more Pythonic way.

In this blog post, we will explore how to filter and query data using SQLAlchemy. We will cover various filtering techniques to query data based on specific conditions.

## Table of Contents
- [Setup](#setup)
- [Filtering Data](#filtering-data)
  - [Simple Filtering](#simple-filtering)
  - [Compound Filtering](#compound-filtering)
  - [Filtering with Operators](#filtering-with-operators)
  - [Filtering with LIKE](#filtering-with-like)
- [Querying Data](#querying-data)
  - [Basic Queries](#basic-queries)
  - [Sorting](#sorting)
  - [Limiting Results](#limiting-results)
- [Conclusion](#conclusion)

## Setup
Before we get started, make sure you have SQLAlchemy installed. You can install it using pip:

```
pip install SQLAlchemy
```

Also, make sure to connect SQLAlchemy to your database by configuring the database URL.

## Filtering Data

### Simple Filtering
Let's say we have a `User` table with columns `id`, `name`, and `age`. To filter users by age greater than 25, we can use the `filter()` method:

```python
users = session.query(User).filter(User.age > 25).all()
```

This will retrieve all users whose age is greater than 25.

### Compound Filtering
You can combine multiple conditions using `and_` or `or_`:

```python
users = session.query(User).filter(User.age > 25, User.name.startswith('J')).all()
```

This will retrieve all users whose age is greater than 25 and their name starts with 'J'.

### Filtering with Operators
SQLAlchemy provides various operators to perform advanced filtering, such as `in_`, `like`, `ilike`, `startswith`, `endswith`, etc.

```python
from sqlalchemy import or_

users = session.query(User).filter(or_(User.name.like('%hello%'), User.age.between(18, 30))).all()
```

This will retrieve all users whose name contains 'hello' or age is between 18 and 30.

### Filtering with LIKE
To perform case-insensitive filtering, you can use the `ilike` operator:

```python
users = session.query(User).filter(User.name.ilike('john%')).all()
```

This will retrieve all users whose name starts with 'John', regardless of case.

## Querying Data

### Basic Queries
In addition to filtering, SQLAlchemy also allows you to perform basic queries. For example, to retrieve all users, you can simply do:

```python
users = session.query(User).all()
```

### Sorting
To sort the results, you can use the `order_by()` method:

```python
users = session.query(User).order_by(User.name.asc()).all()
```

This will retrieve all users sorted in ascending order by their name.

### Limiting Results
If you only want to retrieve a subset of results, you can use the `limit()` method:

```python
users = session.query(User).limit(10).all()
```

This will retrieve only the first 10 users.

## Conclusion
In this blog post, we learned how to filter and query data using SQLAlchemy. We explored various filtering techniques, such as simple filtering, compound filtering, filtering with operators, and filtering with LIKE. We also covered basic querying, sorting, and limiting results.

SQLAlchemy provides a powerful and flexible way to interact with databases in Python. By mastering filtering and querying techniques, you can efficiently retrieve the data you need from your database.