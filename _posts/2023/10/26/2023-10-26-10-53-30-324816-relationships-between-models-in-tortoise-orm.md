---
layout: post
title: "[python] Relationships between models in Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Tortoise ORM is a powerful Object-Relational Mapping (ORM) library for Python, designed to simplify database interactions. One of the fundamental aspects of an ORM is the ability to define relationships between different models/classes, enabling the representation of complex data structures.

In this blog post, we will explore the various types of relationships supported by Tortoise ORM and how to implement them in your Python applications.

## Table of Contents

- [Introduction](#introduction)
- [One-to-One Relationship](#one-to-one-relationship)
- [One-to-Many Relationship](#one-to-many-relationship)
- [Many-to-Many Relationship](#many-to-many-relationship)
- [Conclusion](#conclusion)

## Introduction

Before we dive into the specifics of relationships, let's briefly understand the concept of models in Tortoise ORM. A model represents a database table, and each instance of the model corresponds to a row in the table. Models are defined as Python classes that inherit from the `Model` class provided by Tortoise ORM.

## One-to-One Relationship

A one-to-one relationship is a relationship where one instance of a model is related to exactly one instance of another model. This relationship can be represented by a foreign key column on either side.

To define a one-to-one relationship in Tortoise ORM, you can use the `OneToOneField` field type. Here's an example:

```python
from tortoise import fields, models

class Person(models.Model):
    name = fields.CharField(max_length=50)
    passport = fields.OneToOneField('models.Passport', related_name='person')

class Passport(models.Model):
    number = fields.CharField(max_length=20)
```

In the example above, the `Passport` model has a one-to-one relationship with the `Person` model. The `passport` field in the `Person` model represents the foreign key relationship.

## One-to-Many Relationship

A one-to-many relationship is a relationship where one instance of a model is related to multiple instances of another model. This relationship can be represented by a foreign key column on the "many" side.

In Tortoise ORM, you can use the `ForeignKeyField` field type to define a one-to-many relationship. Here's an example:

```python
from tortoise import fields, models

class Author(models.Model):
    name = fields.CharField(max_length=50)

class Book(models.Model):
    title = fields.CharField(max_length=100)
    author = fields.ForeignKeyField('models.Author', related_name='books')
```

In the example above, the `Author` model has a one-to-many relationship with the `Book` model. The `author` field in the `Book` model represents the foreign key relationship.

## Many-to-Many Relationship

A many-to-many relationship is a relationship where one instance of a model is related to multiple instances of another model, and vice versa. This relationship requires an intermediate table to store the associations between the two models.

To define a many-to-many relationship in Tortoise ORM, you can use the `ManyToManyField` field type. Here's an example:

```python
from tortoise import fields, models

class Tag(models.Model):
    name = fields.CharField(max_length=50)

class Article(models.Model):
    title = fields.CharField(max_length=100)
    tags = fields.ManyToManyField('models.Tag', related_name='articles')
```

In the example above, the `Article` model has a many-to-many relationship with the `Tag` model. The `tags` field in the `Article` model represents the many-to-many relationship.

## Conclusion

Tortoise ORM provides a comprehensive set of features for defining and managing relationships between models. Whether it's a one-to-one, one-to-many, or many-to-many relationship, Tortoise ORM makes it easy to work with complex data structures and perform efficient database operations.

References:
- [Tortoise ORM Documentation](https://tortoise-orm.readthedocs.io)
- [Python](https://www.python.org/)