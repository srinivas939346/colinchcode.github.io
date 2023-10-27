---
layout: post
title: "[python] Creating Django models and database migrations"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

In Django, models are used to define the structure of the database tables. They represent the data that will be stored in the tables and provide a convenient way to interact with the database. 

Migrations, on the other hand, are used to keep track of database schema changes. They allow you to update the database structure without losing any existing data. 

In this blog post, we will walk through the process of creating models and applying database migrations in Django.

## Table of Contents
- [Defining Models](#defining-models)
	- [Fields](#fields)
	- [Relationships](#relationships)
- [Creating Migrations](#creating-migrations)
- [Applying Migrations](#applying-migrations)
- [Conclusion](#conclusion)

## Defining Models

To define a model in Django, you need to create a new Python class that inherits from the `django.db.models.Model` base class. Each attribute of the class represents a field in the database table.

### Fields

Django provides a wide range of field types to choose from, depending on the type of data you want to store. Some common field types include:

- `CharField`: used to store a string of characters.
- `IntegerField`: used to store an integer value.
- `BooleanField`: used to store a boolean value.
- `DateTimeField`: used to store date and time information.

Here's an example of a model with different field types:

```python
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.CharField(max_length=50)
    publication_date = models.DateTimeField()
    is_available = models.BooleanField(default=True)
```

### Relationships

Django supports various types of relationships between models, such as one-to-one, one-to-many, and many-to-many relationships.

- `ForeignKey`: used to define a one-to-many relationship.
- `OneToOneField`: used to define a one-to-one relationship.
- `ManyToManyField`: used to define a many-to-many relationship.

Here's an example of a model with a foreign key relationship:

```python
from django.db import models

class Category(models.Model):
    name = models.CharField(max_length=50)

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.CharField(max_length=50)
    publication_date = models.DateTimeField()
    category = models.ForeignKey(Category, on_delete=models.CASCADE)
```

## Creating Migrations

Once you have defined your models, you need to create migrations. Migrations are files that Django uses to track and apply changes to the database schema.

To create a migration, open the command prompt or terminal and navigate to the project directory. Then run the following command:

```
python manage.py makemigrations
```

Django will automatically generate a migration file based on the changes you have made to your models.

## Applying Migrations

To apply the migrations and update the database, run the following command:

```
python manage.py migrate
```

Django will execute the migrations in the order they were created and update the database accordingly.

## Conclusion

In this blog post, we have covered the basics of creating Django models and applying database migrations. Models define the structure of the database tables, while migrations keep track of schema changes. By following these steps, you can easily create and maintain your database structure in Django.

References:
- [Django Documentation - Models](https://docs.djangoproject.com/en/3.2/topics/db/models/)
- [Django Documentation - Migrations](https://docs.djangoproject.com/en/3.2/topics/migrations/)