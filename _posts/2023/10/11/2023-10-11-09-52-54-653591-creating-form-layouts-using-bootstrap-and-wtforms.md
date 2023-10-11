---
layout: post
title: "[python] Creating form layouts using Bootstrap and WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

When it comes to creating form layouts for web applications, using a combination of Bootstrap and WTForms can make the process much easier and efficient. Bootstrap is a popular front-end framework that provides pre-designed components and a responsive grid system, while WTForms is a library for building web forms in Python.

In this tutorial, we will walk through the steps of creating a form layout using Bootstrap and integrating it with WTForms in a Python application.

## Table of Contents
1. [Setting up the environment](#setting-up-the-environment)
2. [Installing Bootstrap](#installing-bootstrap)
3. [Creating a simple form with WTForms](#creating-a-simple-form-with-wtforms)
4. [Integrating Bootstrap classes with form fields](#integrating-bootstrap-classes-with-form-fields)
5. [Adding form validation](#adding-form-validation)
6. [Conclusion](#conclusion)

## 1. Setting up the environment<a name="setting-up-the-environment"></a>

Before we start, make sure you have Python and pip installed on your system. You will also need a virtual environment to keep your project dependencies isolated. If you don't have virtualenv installed, you can install it using pip:

```
pip install virtualenv
```

Once you have virtualenv installed, create a new virtual environment for your project:

```
virtualenv myenv
```

Activate the virtual environment:

```
source myenv/bin/activate (Unix)
myenv\Scripts\activate (Windows)
```

## 2. Installing Bootstrap<a name="installing-bootstrap"></a>

To work with Bootstrap, we need to include the necessary CSS and JavaScript files in our HTML templates. The easiest way to do this is by using a CDN (Content Delivery Network).

Add the following lines to the `<head>` section of your HTML template(s):

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
```

## 3. Creating a simple form with WTForms<a name="creating-a-simple-form-with-wtforms"></a>

Start by installing the WTForms library using pip:

```
pip install wtforms
```

Create a new Python file, for example, `app.py`, and import the necessary modules:

```python
from flask import Flask, render_template
from flask_wtf import FlaskForm
from wtforms import StringField, PasswordField, SubmitField
```

Next, create a form class by subclassing `FlaskForm`:

```python
class LoginForm(FlaskForm):
    username = StringField('Username')
    password = PasswordField('Password')
    submit = SubmitField('Sign In')
```

## 4. Integrating Bootstrap classes with form fields<a name="integrating-bootstrap-classes-with-form-fields"></a>

With the form class defined, we can now create an HTML template and integrate Bootstrap classes with the form fields. Create a new file named `login.html` in a templates folder.

Start by extending the base Bootstrap template and importing the necessary macros:

```html
{% extends 'bootstrap/base.html' %}
{% import 'bootstrap/wtf.html' as wtf %}
```

In the body section of the template, add the form fields using the provided macros:

```html
{% block content %}
  <div class="container">
    <h1>Login Form</h1>
    <hr>
    {{ wtf.quick_form(form) }}
  </div>
{% endblock %}
```

## 5. Adding form validation<a name="adding-form-validation"></a>

WTForms provides built-in form validation capabilities. Add some validation rules to the `LoginForm` class in `app.py`:

```python
from wtforms.validators import DataRequired, Length

class LoginForm(FlaskForm):
    username = StringField('Username', validators=[DataRequired(), Length(min=4, max=25)])
    password = PasswordField('Password', validators=[DataRequired()])
    submit = SubmitField('Sign In')
```

With the validation rules in place, any empty fields or fields that do not meet the specified criteria will trigger form validation errors.

## 6. Conclusion<a name="conclusion"></a>

In this tutorial, we have learned how to create form layouts using Bootstrap and integrate them with WTForms in a Python application. We have covered setting up the environment, installing Bootstrap, creating a simple form with WTForms, and adding form validation.

This combination of Bootstrap and WTForms allows us to quickly build responsive and user-friendly forms while leveraging the power of Python. By following these steps, you can create professional-looking forms that are easy to maintain and customize.

Remember to always refer to the official documentation of Bootstrap and WTForms for more advanced features and customization options.

Happy coding!