---
layout: post
title: "[python] Using WTForms with FastAPI"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

In this post, we'll explore how to use **WTForms** with **FastAPI**, a modern, fast, web framework for building APIs with Python. 

## Table of Contents
- [What is WTForms?](#what-is-wtforms)
- [Setting Up FastAPI](#setting-up-fastapi)
- [Installing WTForms](#installing-wtforms)
- [Creating a Form with WTForms](#creating-a-form-with-wtforms)
- [Validating Form Data](#validating-form-data)
- [Rendering the Form](#rendering-the-form)
- [Conclusion](#conclusion)

## What is WTForms?

**WTForms** is a flexible forms validation and rendering library for Python web development. It is widely used to build web forms in frameworks like Flask and Django.

## Setting Up FastAPI

If you haven't yet installed **FastAPI**, you can do so using `pip`:

```
$ pip install fastapi
```

Once FastAPI is installed, we can start building our application.

## Installing WTForms

To use WTForms in our FastAPI application, we need to install the `wtforms` package:

```
$ pip install wtforms
```

## Creating a Form with WTForms

To get started with WTForms, let's create a simple form to collect user information. We'll create a new file called `forms.py` and define our form there:

```python
from wtforms import Form, StringField, IntegerField, validators

class UserForm(Form):
    name = StringField('Name', [validators.DataRequired()])
    age = IntegerField('Age', [validators.DataRequired(), validators.NumberRange(min=18, max=99)])
    email = StringField('Email', [validators.DataRequired(), validators.Email()])
```

In the above code, we define a `UserForm` class that inherits from `Form` provided by WTForms. We specify the fields of the form using various field types from WTForms, along with the necessary validators.

## Validating Form Data

To validate the form data in our FastAPI application, we can create a route and use the `UserForm` class to validate the data. Here's an example:

```python
from fastapi import FastAPI
from forms import UserForm

app = FastAPI()

@app.post("/user")
async def create_user(user_form: UserForm):
    if user_form.validate():
        # Process the validated user data
        return {"message": "User created successfully"}
    else:
        # Handle form validation errors
        return {"message": "Form validation failed"}
```

In the above code, we define a route `/user` that expects a `POST` request with the `UserForm` data. We call the `validate()` method on the form instance to validate the data. If the data is valid, we can proceed with processing it, otherwise, we return a validation error message.

## Rendering the Form

To render the form in an HTML template, we can use the WTForms rendering functionality. Here's an example of rendering the `UserForm` in a Flask template (assuming you have Flask installed):

```python
from flask import Flask, render_template
from forms import UserForm

app = Flask(__name__)

@app.route("/")
def show_form():
    form = UserForm()
    return render_template("form.html", form=form)
```

In the above code, we create an instance of the `UserForm` and pass it to the template for rendering. In the template, you can use WTForms macros to render the form fields, validation errors, etc.

## Conclusion

In this post, we learned how to use WTForms with FastAPI to create, validate, and render forms in our web application. WTForms provides a convenient way to handle form data validation and rendering, allowing us to focus more on the application logic.