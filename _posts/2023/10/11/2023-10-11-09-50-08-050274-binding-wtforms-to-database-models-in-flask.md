---
layout: post
title: "[python] Binding WTForms to database models in Flask"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

Flask is a popular web development framework in Python that allows developers to easily build web applications. One key aspect of web development is handling forms, and Flask provides an extension called WTForms that makes form validation and rendering smoother.

WTForms is a flexible forms validation and rendering library in Python, which allows developers to create forms using classes and bind them to database models. This enables automatic population of form fields with values from the model, as well as data validation and handling of form submissions.

In this article, we will explore how to bind WTForms to database models in Flask, using SQLAlchemy as the database tool.

## Table of Contents:
- [Setting up the Environment](#setting-up-the-environment)
- [Creating the Database Model](#creating-the-database-model)
- [Creating the Flask Form](#creating-the-flask-form)
- [Rendering the Form](#rendering-the-form)
- [Handling Form Submission](#handling-form-submission)

## Setting up the Environment

To get started, make sure you have Flask, WTForms, and SQLAlchemy installed in your Python environment. You can install them using pip:

```shell
$ pip install Flask WTForms SQLAlchemy
```

## Creating the Database Model

Let's assume we have a simple `User` model that represents users in our application. We will use SQLAlchemy to define the model and handle interactions with the database.

```python
from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(50), nullable=False)
    email = db.Column(db.String(120), unique=True, nullable=False)
    password = db.Column(db.String(80), nullable=False)
```

## Creating the Flask Form

Now, we need to create a Flask form that will bind to our `User` model. WTForms provides various fields such as `StringField`, `PasswordField`, `BooleanField`, etc., that can be used to create form fields.

```python
from flask_wtf import FlaskForm
from wtforms import StringField, PasswordField
from wtforms.validators import DataRequired, Email

class UserForm(FlaskForm):
    name = StringField('Name', validators=[DataRequired()])
    email = StringField('Email', validators=[DataRequired(), Email()])
    password = PasswordField('Password', validators=[DataRequired()])
```

In the above code, we have defined a `UserForm` class that inherits from `FlaskForm`. It has form fields such as `name`, `email`, and `password`, along with validation rules using WTForms validators.

## Rendering the Form

To render the form in a Flask view, we need to create an instance of the form and pass it to the template. Let's assume we have a `create_user` view that renders a template to create a new user.

```python
from flask import Flask, render_template

app = Flask(__name__)
app.config['SECRET_KEY'] = 'your-secret-key'

@app.route('/user/create', methods=['GET', 'POST'])
def create_user():
    form = UserForm()

    if form.validate_on_submit():
        # Handle form submission and create a new user
        user = User(name=form.name.data, email=form.email.data, password=form.password.data)
        db.session.add(user)
        db.session.commit()
        return 'User created successfully!'

    return render_template('create_user.html', form=form)
```

In the above code, we create an instance of `UserForm` called `form`. The `validate_on_submit` method checks if the form has been submitted and validates the form data. If validation passes, a new `User` object is created and added to the database.

## Handling Form Submission

Finally, we need to create a template to render the form and handle form submissions. Here's an example template `create_user.html`:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Create User</title>
  </head>
  <body>
    <h1>Create User</h1>
    <form method="POST" action="{{ url_for('create_user') }}">
      {{ form.csrf_token }}
      {{ form.name.label }}: {{ form.name() }}<br>
      {{ form.email.label }}: {{ form.email() }}<br>
      {{ form.password.label }}: {{ form.password() }}<br>
      <input type="submit" value="Create">
    </form>
  </body>
</html>
```

In the above template, `{{ form.name }}`, `{{ form.email }}`, and `{{ form.password }}` render the corresponding form fields. The `form.csrf_token` is a security measure to protect against CSRF attacks.

That's it! We have successfully bound WTForms to our database model in Flask. Now you can create forms based on your database models and easily handle validation and form submissions.