---
layout: post
title: "[python] Building a REST API with Django and Django REST framework"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to build a REST API using Django, a popular Python web framework, and Django REST framework (DRF), a powerful toolkit for building web APIs. By the end of this tutorial, you will have a working understanding of how to create a RESTful API with Django and DRF.

## Table of Contents
- [Introduction](#introduction)
- [Setting up a Django Project](#setting-up-a-django-project)
- [Creating Models](#creating-models)
- [Serializers](#serializers)
- [Views](#views)
- [Using the API](#using-the-api)

## Introduction

REST (Representational State Transfer) is a software architectural style that defines a set of constraints to be used when creating web services. A RESTful API allows different software applications to communicate with each other by using standard HTTP methods such as GET, POST, PUT, and DELETE. Django, with the help of Django REST framework, makes it easy to build RESTful APIs.

## Setting up a Django Project

To get started, you will need to have Django and Django REST framework installed. You can install them by running the following commands:

```bash
pip install django
pip install djangorestframework
```

Once you have Django and DRF installed, you can create a new Django project by running the following command:

```bash
django-admin startproject myproject
```

This will create a new directory named `myproject` with the basic structure of a Django project.

## Creating Models

In Django, models are used to define the structure and behavior of your data. To create models for our REST API, let's say we want to build an API for managing a list of books. We can define a `Book` model in `myapp/models.py` file:

```python
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.CharField(max_length=100)
    publication_date = models.DateField()
```

## Serializers

Serializers in DRF provide a way to convert complex data types, such as Django models, into JSON or other formats that can be easily rendered into responses. Let's create a serializer for our `Book` model:

```python
from rest_framework import serializers
from myapp.models import Book

class BookSerializer(serializers.ModelSerializer):
    class Meta:
        model = Book
        fields = ['id', 'title', 'author', 'publication_date']
```

## Views

In Django, views are responsible for handling HTTP requests and returning HTTP responses. In our case, we need to create views for our API endpoints. We can create a file `myapp/views.py` and define the views as follows:

```python
from rest_framework import generics
from myapp.models import Book
from myapp.serializers import BookSerializer

class BookList(generics.ListCreateAPIView):
    queryset = Book.objects.all()
    serializer_class = BookSerializer

class BookDetail(generics.RetrieveUpdateDestroyAPIView):
    queryset = Book.objects.all()
    serializer_class = BookSerializer
```

## Using the API

To start the development server and test our API, use the following command:

```bash
python manage.py runserver
```

Now you can access your API at `http://localhost:8000/api/books`. You should be able to perform various actions like creating, updating, deleting, and retrieving books.

Congratulations! You have successfully built a REST API using Django and Django REST framework. This is just a simple example, but it should give you a good foundation to start building more complex APIs. For more advanced features, make sure to check out the official Django REST framework documentation.

## References
- [Django Documentation](https://www.djangoproject.com/)
- [Django REST framework Documentation](https://www.django-rest-framework.org/)