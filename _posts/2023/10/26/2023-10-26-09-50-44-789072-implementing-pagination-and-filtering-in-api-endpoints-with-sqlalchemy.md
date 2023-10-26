---
layout: post
title: "[python] Implementing pagination and filtering in API endpoints with SQLAlchemy"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When building APIs, it is common to have endpoints that return a large number of records. To improve performance and enhance user experience, implementing pagination and filtering becomes crucial. In this blog post, we will explore how to achieve pagination and filtering in API endpoints using SQLAlchemy, a popular Object-Relational Mapping (ORM) library for Python.

## Prerequisites

To follow along, make sure you have the following requirements set up:

- Python installed on your machine
- A relational database (e.g., MySQL or PostgreSQL) with some data
- SQLAlchemy and the relevant database driver installed (e.g., `psycopg2` for PostgreSQL)

## Setting up SQLAlchemy

Before we dive into pagination and filtering, let's set up SQLAlchemy in our project. Start by installing SQLAlchemy using the following command:

```shell
pip install sqlalchemy
```

Next, import the required modules in your Python script:

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker
from sqlalchemy.ext.declarative import declarative_base
```

Then, define the database connection URL and create the engine to connect to your database:

```python
DATABASE_URL = "postgresql://username:password@localhost/database"
engine = create_engine(DATABASE_URL)
```

Finally, create a `Session` class using `sessionmaker` and bind it to the engine:

```python
Session = sessionmaker(bind=engine)
session = Session()
```

With these initial steps, SQLAlchemy is set up to interact with your database.

## Pagination

Pagination allows us to split large result sets into smaller pages, preventing the API from returning all records at once. SQLAlchemy provides convenient methods to achieve pagination effortlessly.

Let's say we have an `Item` table in our database, and we want to fetch a paginated list of items. We can use the following code:

```python
from sqlalchemy import func
from sqlalchemy.orm import query

class Item(Base):
    __tablename__ = "items"

    id = Column(Integer, primary_key=True)
    name = Column(String)
    price = Column(Float)

def paginate_items(page: int = 1, page_size: int = 10) -> query.Query:
    query = session.query(Item)
    total_count = query.count()

    query = query.offset((page - 1) * page_size)
    query = query.limit(page_size)

    return query.all(), total_count
```

In the code above, we define a SQLAlchemy model `Item` representing the database table. The `paginate_items()` function takes two parameters: `page` and `page_size`. It calculates the total count of items and applies the `offset` and `limit` clause to the query to retrieve the desired page of items.

To use this function, call `paginate_items()` with the desired page number and page size:

```python
items, total_count = paginate_items(page=1, page_size=10)
```

This will return a list of items for the specified page along with the total count of all items.

## Filtering

Filtering allows us to retrieve specific records based on certain conditions. SQLAlchemy provides a powerful query API to construct complex filters effortlessly.

To add filtering support to our API endpoint, let's extend our `paginate_items()` function to accept additional filter parameters:

```python
from sqlalchemy import or_, and_

def paginate_items(page: int = 1, page_size: int = 10, min_price: float = None, max_price: float = None) -> query.Query:
    query = session.query(Item)
    total_count = query.count()

    if min_price is not None:
        query = query.filter(Item.price >= min_price)
    if max_price is not None:
        query = query.filter(Item.price <= max_price)

    query = query.offset((page - 1) * page_size)
    query = query.limit(page_size)

    return query.all(), total_count
```

In the enhanced code, we added two optional parameters `min_price` and `max_price` to the function. If these parameters are provided, the function adds filters to the query to retrieve items within the provided price range.

To use the filtering feature, call the `paginate_items()` function with the desired filter values:

```python
items, total_count = paginate_items(page=1, page_size=10, min_price=10.0, max_price=50.0)
```

This will return a paginated list of items with prices ranging from 10.0 to 50.0.

## Conclusion

In this blog post, we explored how to implement pagination and filtering in API endpoints using SQLAlchemy. We learned how to set up SQLAlchemy, handle pagination, and apply filters to our queries effortlessly. By incorporating these features, we can optimize performance and improve the user experience of our API endpoints.

By leveraging the power of SQLAlchemy, handling large datasets becomes more manageable, ensuring that the API remains responsive and efficient.

**References:**
- [SQLAlchemy Documentation](https://docs.sqlalchemy.org/)
- [SQLAlchemy Pagination Tutorial](https://docs.sqlalchemy.org/en/14/orm/tutorial.html#paging-and-eager-loading)