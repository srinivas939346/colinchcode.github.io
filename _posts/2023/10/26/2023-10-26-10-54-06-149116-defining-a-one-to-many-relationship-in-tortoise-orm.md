---
layout: post
title: "[python] Defining a one-to-many relationship in Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Tortoise ORM is an easy-to-use and powerful Python object-relational mapping (ORM) library. It provides a simple syntax to define and work with database models in an asynchronous environment. In this blog post, we will explore how to define a one-to-many relationship using Tortoise ORM.

## Table of Contents
1. [Introduction](#introduction)
2. [Defining the Models](#defining-the-models)
3. [Working with the Relationship](#working-with-the-relationship)
4. [Conclusion](#conclusion)

## Introduction<a name="introduction"></a>

In a one-to-many relationship, one record in the first table can be related to multiple records in the second table. In the context of Tortoise ORM, this means that one instance of a model can be associated with multiple instances of another model.

To establish a one-to-many relationship, we need to define the models that represent the two tables involved. We will create two models: `Author` and `Book`. Each author can have multiple books associated with them.

## Defining the Models<a name="defining-the-models"></a>

Let's start by creating the `Author` model. Open your Python file and import `models` from `tortoise` package.

```python
from tortoise import models, fields


class Author(models.Model):
    name = fields.CharField(max_length=255)
    books = fields.ReverseRelation["Book"]

    def __str__(self):
        return self.name
```

In this code snippet, we define the `Author` model with a `name` field of type `CharField` to store the author's name. Additionally, we define a reverse relationship `books` to represent the one-to-many relationship between `Author` and `Book` models.

Next, let's create the `Book` model. We will import the `Author` model and define a foreign key to establish the relationship.

```python
class Book(models.Model):
    title = fields.CharField(max_length=255)
    author = fields.ForeignKeyField("models.Author", related_name="books")

    def __str__(self):
        return self.title
```

In the `Book` model, we define a `title` field of type `CharField` to store the book's title. We also define a foreign key `author` that references the `Author` model using the `related_name` parameter. This establishes the one-to-many relationship between the two models.

## Working with the Relationship<a name="working-with-the-relationship"></a>

Once the models are defined, you can use them to create, query, and manipulate the data in the database. Here's an example of how to create an author and associate multiple books with them:

```python
async def create_author_with_books():
    author = await Author.create(name="John Doe")
    await Book.create(title="Book 1", author=author)
    await Book.create(title="Book 2", author=author)
    await Book.create(title="Book 3", author=author)
```

In this example, we create an instance of the `Author` model with the name "John Doe". Then, we use the `create()` method of the `Book` model to create three books and associate them with the author by passing the `author` parameter.

To retrieve the books associated with an author, you can simply access the `books` attribute of an `Author` instance:

```python
async def get_books_of_author(author_id):
    author = await Author.get(id=author_id)
    books = author.books
    for book in books:
        print(book.title)
```

In this code snippet, we retrieve the `Author` instance with a specific `id` and access the `books` attribute to get all the books associated with that author. We then iterate over the books and print their titles.

## Conclusion<a name="conclusion"></a>

Defining a one-to-many relationship in Tortoise ORM is straightforward. By properly defining models and relationships, you can easily work with related data and perform operations on them. Whether you are building a small application or a complex system, Tortoise ORM provides a convenient way to establish and manage these relationships.

To learn more about Tortoise ORM and its features, refer to the official documentation: [Tortoise ORM Documentation](https://tortoise-orm.readthedocs.io/)

Happy coding!