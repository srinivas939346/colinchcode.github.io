---
layout: post
title: "[python] Handling form data in Tornado using WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

When building web applications with Tornado, it's common to have forms that allow users to input data. To handle this form data and perform validation, we can use WTForms, a flexible forms validation and rendering library.

In this blog post, we will walk through the process of handling form data in Tornado using WTForms. We will cover form creation, validation, and rendering.

## Table of Contents
1. [Installing WTForms](#installing-wtforms)
2. [Creating a form](#creating-a-form)
3. [Handling form submission](#handling-form-submission)
4. [Rendering the form](#rendering-the-form)

## 1. Installing WTForms

First, let's install WTForms using pip:

```python
pip install wtforms
```

## 2. Creating a form

To create a form using WTForms, we need to define a class that inherits from the `wtforms.Form` class. Each form field is represented by an instance of a `wtforms.Field` subclass.

Let's create a simple form with two fields: `name` and `email`. The `TextField` class is used to represent a text input field, and the `EmailField` class is used to validate email addresses.

```python
from wtforms import Form, TextField, EmailField

class MyForm(Form):
    name = TextField('Name')
    email = EmailField('Email')
```

## 3. Handling form submission

To handle form submission in Tornado, we can define a request handler that inherits from `tornado.web.RequestHandler`. We can then instantiate our form class and use the `get_argument` method to retrieve the form data submitted by the user.

```python
import tornado.web

class FormHandler(tornado.web.RequestHandler):
    def post(self):
        form = MyForm(self.request.arguments)
        if form.validate():
            # Form data is valid, process it here
            name = form.name.data
            email = form.email.data
            # ... other processing logic ...
            self.write("Form submitted successfully")
        else:
            # Form data is invalid, handle the error here
            self.write("Invalid form data")
```

In the `post` method, we create an instance of `MyForm` by passing in `self.request.arguments`, which is a dictionary containing the form data submitted by the user. We can then call the `validate` method on the form instance to check if the data is valid. If the data is valid, we can access the submitted values using the `data` attribute of each field.

## 4. Rendering the form

To render the form in a Tornado template, we can pass an instance of our form to the template context. We can then use the `render` method of each field to generate the corresponding HTML code.

```python
import tornado.web

class FormHandler(tornado.web.RequestHandler):
    def get(self):
        form = MyForm()
        self.render("form.html", form=form)
```

In the template (`form.html`), we can use the `render` method of each field to generate the HTML code for the form inputs:

```html
<form method="post" action="/form">
    {{ form.name.label }} {{ form.name() }}<br>
    {{ form.email.label }} {{ form.email() }}<br>
    <input type="submit" value="Submit">
</form>
```

In this example, `form.name.label` and `form.name()` will respectively render the label and text input HTML code for the `name` field.

That's it! You now know how to handle form data in Tornado using WTForms. This allows you to easily validate and process user input in your web applications. Happy coding!