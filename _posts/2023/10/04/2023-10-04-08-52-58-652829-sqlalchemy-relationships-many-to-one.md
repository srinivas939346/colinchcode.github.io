---
layout: post
title: "[python] SQLAlchemy Relationships: Many-to-One"
description: " "
date: 2023-10-04
tags: [python]
comments: true
share: true
---

In the world of relational databases, relationships are essential to represent the connections between different entities or tables. SQLAlchemy, a popular Object-Relational Mapping (ORM) library for Python, provides a convenient way to define and manage these relationships. In this blog post, we will explore the many-to-one relationship in SQLAlchemy.

## Table of Contents

- [Introduction](#introduction)
- [Defining the Relationship](#defining-the-relationship)
- [Querying with Relationships](#querying-with-relationships)
- [Conclusion](#conclusion)

## Introduction

In a many-to-one relationship, multiple records in one table can be associated with a single record in another table. For example, consider a scenario where we have two tables: `Author` and `Book`, where an author can write multiple books, but a book can only have one author. Here, the relationship is many books to one author.

## Defining the Relationship

To define a many-to-one relationship in SQLAlchemy, we need to use the `relationship` function provided by SQLAlchemy. Let's see how to define this relationship in code:

```python
from sqlalchemy import Column, ForeignKey, Integer, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import relationship

Base = declarative_base()

class Author(Base):
    __tablename__ = 'authors'
    id = Column(Integer, primary_key=True)
    name = Column(String)
    books = relationship("Book", back_populates="author")

class Book(Base):
    __tablename__ = 'books'
    id = Column(Integer, primary_key=True)
    title = Column(String)
    author_id = Column(Integer, ForeignKey('authors.id'))
    author = relationship("Author", back_populates="books")
```

In the above code, we define two classes `Author` and `Book` as SQLAlchemy models. Inside the `Author` class, we define a `books` attribute of type `relationship` which represents the many-to-one relationship between `Author` and `Book` classes. Similarly, inside the `Book` class, we define an `author` attribute of type `relationship` to establish the inverse relationship.

## Querying with Relationships

Once we have defined the many-to-one relationship, we can easily query and access related objects using dot notation. Let's take a look at some example queries:

```python
# Query all books written by an author
author = session.query(Author).filter(Author.name == "John Doe").first()
books = author.books  # Access the books using the relationship attribute

# Query the author of a book
book = session.query(Book).filter(Book.title == "Python Mastery").first()
author = book.author  # Access the author using the relationship attribute
```

In the first query, we retrieve the `Author` object with the name "John Doe" and access the related books using the `books` attribute defined in the `Author` class. Similarly, in the second query, we retrieve the `Book` object with the title "Python Mastery" and access the related author using the `author` attribute defined in the `Book` class.

## Conclusion

In this blog post, we explored the many-to-one relationship in SQLAlchemy. We learned how to define and manage this type of relationship using the `relationship` function. We also saw how to query and access related objects using the relationship attributes. SQLAlchemy provides a powerful and intuitive way to work with relational databases and handle complex relationships with ease.