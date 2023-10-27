---
layout: post
title: "[python] Understanding Django models"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Django is a popular web framework written in Python, and one of its core components is the models module. Models in Django provide an easy way to define the structure and behavior of your data.

## Table of Contents
- [What is a Model?](#what-is-a-model)
- [Defining Models](#defining-models)
- [Fields and Relationships](#fields-and-relationships)
- [Model Methods](#model-methods)
- [Querying and Saving Data](#querying-and-saving-data)
- [References](#references)

## What is a Model?

A model in Django is a Python class that represents a table in the database. It provides an abstraction layer over the underlying database structure, allowing you to interact with the data using Python code instead of direct SQL queries.

## Defining Models

To define a model in Django, you need to create a new class that inherits from the `django.db.models.Model` class. Each attribute of the class represents a field in the database table. For example, if you want to create a model for a blog post, you might define it like this:

```python
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    pub_date = models.DateTimeField(auto_now_add=True)
```

In the above code, we define a `Post` model with three fields: `title`, `content`, and `pub_date`. The `CharField` represents a string field, `TextField` represents a longer text field, and `DateTimeField` represents a date and time field. The `auto_now_add=True` parameter automatically sets the current datetime when a new post is created.

## Fields and Relationships

Django provides a wide range of field types that you can use to define your models. Some common field types include `CharField`, `IntegerField`, `BooleanField`, `ForeignKey`, and `ManyToManyField`. These field types allow you to define various data types and relationships between models.

For example, you can define a foreign key relationship between a `Post` model and a `User` model like this:

```python
class Post(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    author = models.ForeignKey(User, on_delete=models.CASCADE)
```

In the above code, the `author` field is a foreign key to the `User` model. The `on_delete=models.CASCADE` parameter specifies that if a user is deleted, all their associated posts will also be deleted.

## Model Methods

Models in Django can also have custom methods that perform actions on the data. These methods can be used to manipulate or retrieve data specific to the model.

```python
class Post(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    pub_date = models.DateTimeField(auto_now_add=True)

    def display_date(self):
        return self.pub_date.strftime("%B %d, %Y")
```

In the above code, we define a `display_date` method that formats the `pub_date` field as a string in a specific format.

## Querying and Saving Data

Once you have defined your models, you can use them to query data from the database and save new data.

```python
# Querying data
posts = Post.objects.all() # Get all blog posts
recent_posts = Post.objects.filter(pub_date__gte=timezone.now()-timedelta(days=7)) # Get posts published in the last 7 days

# Saving data
new_post = Post(title="New Post", content="Lorem ipsum dolor sit amet.")
new_post.save()
```

In the above code, we use the `objects` attribute of the `Post` model to perform database queries. The `all()` method returns all objects of the model, and the `filter()` method allows you to apply filters to the query.

To save a new object to the database, we create an instance of the model and call the `save()` method.

## References

1. Django documentation: [Models](https://docs.djangoproject.com/en/3.1/topics/db/models/)
2. Django documentation: [Field Types](https://docs.djangoproject.com/en/3.1/ref/models/fields/)
3. Django documentation: [Making Queries](https://docs.djangoproject.com/en/3.1/topics/db/queries/)