---
layout: post
title: "[python] Using WTForms within Django REST Framework"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

## Introduction

When building a web application using Django, forms are an essential component for data validation and user input. Django provides its own form handling mechanism, but another popular option is to use **WTForms**, a flexible form library for Python.

**Django REST Framework** (DRF) is a powerful toolkit for building web APIs in Django. It provides serialization, authentication, and request/response handling out of the box. In this article, we will explore how to integrate WTForms with DRF to handle form validation in a Django REST API.

## Prerequisites

Before we start, make sure you have the following installed:

- Python (version 3.6+)
- Django (version 3.0+)
- Django REST Framework (version 3.11+)
- WTForms (version 2.3+)

You can install these dependencies using pip:

```shell
pip install Django djangorestframework WTForms
```

## Setup

First, create a new Django project and app by running the following commands:

```shell
django-admin startproject myproject
cd myproject
python manage.py startapp myapp
```

Next, add `rest_framework` and `myapp` to the `INSTALLED_APPS` list in the `settings.py` file of your project.

```python
# settings.py

INSTALLED_APPS = [
    ...
    'rest_framework',
    'myapp',
    ...
]
```

## Creating a WTForms form

Create a new file named `forms.py` within your `myapp` directory. In this file, we will define a simple WTForms form class.

```python
# forms.py

from wtforms import Form, StringField, SubmitField


class MyForm(Form):
    name = StringField('Name')
    email = StringField('Email')
    submit = SubmitField('Submit')
```

## Serializing the form with DRF

Next, we'll create a serializer in Django REST Framework to serialize our form fields.

Create a new file named `serializers.py` within your `myapp` directory and add the following code:

```python
# serializers.py

from rest_framework import serializers
from .forms import MyForm


class MyFormSerializer(serializers.Serializer):
    name = serializers.CharField()
    email = serializers.EmailField()
```

## Creating an API view

Now, let's create a DRF view to handle our form submission. In the `views.py` file, add the following code:

```python
# views.py

from rest_framework.views import APIView
from rest_framework.response import Response
from .forms import MyForm
from .serializers import MyFormSerializer


class MyFormView(APIView):
    def post(self, request):
        form = MyForm(request.POST)
        if form.validate():
            serializer = MyFormSerializer(data=form.data)
            if serializer.is_valid():
                # Do something with the cleaned data
                return Response(serializer.data)
        return Response(form.errors, status=400)
```

## Wiring up the URLs

Finally, we need to wire up our view to a URL in the `urls.py` file.

```python
# urls.py

from django.urls import path
from .views import MyFormView

urlpatterns = [
    path('api/myform/', MyFormView.as_view()),
]
```

## Conclusion

By integrating WTForms with Django REST Framework, we can easily handle form validation in our Django REST API. In this article, we've seen how to create a WTForms form, serialize it using DRF, and handle form submissions via an API view. Feel free to explore WTForms and DRF further to build more complex forms and APIs.

Now you can give it a try and start building powerful and validated forms using WTForms within Django REST Framework!