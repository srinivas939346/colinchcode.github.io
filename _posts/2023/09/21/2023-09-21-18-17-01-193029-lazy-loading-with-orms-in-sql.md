---
layout: post
title: "Lazy loading with ORMs in SQL."
description: " "
date: 2023-09-21
tags: [tech, lazyloading]
comments: true
share: true
---

In modern web development, **Object-Relational Mapping (ORM)** frameworks have become essential for efficient and rapid development. They simplify the process of working with databases, allowing developers to interact with the database using high-level programming constructs instead of writing raw SQL queries.

One important concept in ORMs is **lazy loading**. Lazy loading is a technique that allows an ORM to defer loading related objects until they are actually accessed. This can greatly improve performance by reducing the amount of data fetched from the database at any given time.

Lazy loading is particularly useful when dealing with **one-to-many** or **many-to-many** relationships in the database. In these cases, loading all related objects upfront could result in a large amount of unnecessary data being fetched. Instead, lazy loading allows the ORM to load related objects on-demand, as they are needed.

### How does lazy loading work?

Let's say we have two tables: `Books` and `Authors`. Each book can have one author, but an author can have multiple books. Using an ORM, we can define a relationship between these tables.

When we retrieve a book from the database, the ORM will only fetch the book's attributes initially. The author information will not be fetched until we try to access it. At that point, the ORM will issue a separate query to retrieve the author data and populate the book object.

### Example code

Here's an example using the popular Python ORM, SQLAlchemy, to demonstrate lazy loading.

```python
from sqlalchemy import Column, Integer, String, ForeignKey
from sqlalchemy.orm import relationship

class Book(Base):
    __tablename__ = 'books'

    id = Column(Integer, primary_key=True)
    title = Column(String)
    author_id = Column(Integer, ForeignKey('authors.id'))
    author = relationship('Author', lazy='joined')

class Author(Base):
    __tablename__ = 'authors'

    id = Column(Integer, primary_key=True)
    name = Column(String)
    books = relationship('Book')

# Usage
book = session.query(Book).first()
print(book.title)  # This won't trigger a query to retrieve the author
print(book.author.name)  # This will trigger a separate query to retrieve the author
```

In this example, the `lazy='joined'` argument for the `relationship()` function specifies that the `author` relationship should be lazily loaded. By default, SQLAlchemy uses lazy loading for relationships, so we don't need to explicitly set it if that's the desired behavior.

### Conclusion

Lazy loading is a powerful concept in ORMs that allows for more efficient retrieval of related objects. By loading these objects on-demand, we can avoid unnecessary database queries and improve performance. When working with ORMs, understanding lazy loading can help optimize your code and improve the user experience.

#tech #orm #sql #lazyloading