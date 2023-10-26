---
layout: post
title: "[python] Handling form data and validation in Flask-SQLAlchemy"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Flask-SQLAlchemy is a popular extension in the Flask ecosystem that provides integration between Flask and SQLAlchemy, making it easier to work with databases in Flask applications.

One common task in web development is handling form data and performing validation on that data. In this blog post, we'll explore how to handle form data and perform validation using Flask-SQLAlchemy.

## Table of Contents
- [Setting Up Flask-SQLAlchemy](#setting-up-flask-sqlalchemy)
- [Creating a Model](#creating-a-model)
- [Creating a Form](#creating-a-form)
- [Handling Form Data](#handling-form-data)
- [Performing Validation](#performing-validation)
- [Conclusion](#conclusion)

## Setting Up Flask-SQLAlchemy

First, let's make sure Flask-SQLAlchemy is installed. You can install it using pip:

```
pip install flask-sqlalchemy
```

In your Flask application, you'll need to initialize Flask-SQLAlchemy by creating an instance of the `SQLAlchemy` class and associating it with your Flask app:

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///mydatabase.db'

db = SQLAlchemy(app)
```

Make sure to set the `SQLALCHEMY_DATABASE_URI` configuration option to the URI of your database.

## Creating a Model

Next, let's create a model that will represent the data we want to store in our database. In this example, let's create a simple `User` model with a few fields:

```python
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(80), unique=True, nullable=False)
    email = db.Column(db.String(120), unique=True, nullable=False)
```

This model will create a table called "user" with columns for `id`, `username`, and `email`.

## Creating a Form

To handle form data, we'll use Flask-WTF, an extension that integrates Flask with the popular WTForms library for form handling and validation.

First, install Flask-WTF:

```
pip install flask-wtf
```

Next, create a form class that inherits from `FlaskForm` and define the fields you want in the form:

```python
from flask_wtf import FlaskForm
from wtforms import StringField, SubmitField
from wtforms.validators import DataRequired, Email

class UserForm(FlaskForm):
    username = StringField('Username', validators=[DataRequired()])
    email = StringField('Email', validators=[DataRequired(), Email()])
    submit = SubmitField('Submit')
```

In this example, we've created a form with two fields: `username` and `email`. The `DataRequired` validator ensures that the fields are not submitted empty, and the `Email` validator validates that the email field is in the correct format.

## Handling Form Data

To handle form data in a Flask view function, you can simply instantiate the form class and pass it to the template:

```python
from flask import render_template

@app.route('/user/new', methods=['GET', 'POST'])
def create_user():
    form = UserForm()
    
    if form.validate_on_submit():
        # Create a new user object and populate it with form data
        user = User()
        form.populate_obj(user)
        
        # Add the user object to the database
        db.session.add(user)
        db.session.commit()
        
        return "User created successfully"
    
    return render_template('user_form.html', form=form)
```

In this example, if the form is submitted and passes validation, a new `User` object is created and saved to the database.

## Performing Validation

Flask-WTF provides various validators that you can use to perform additional validation on the form data.

For example, you can add a custom validation method to the form class:

```python
from wtforms.validators import ValidationError

class UserForm(FlaskForm):
    # ...
    
    def validate_username(self, field):
        existing_user = User.query.filter_by(username=field.data).first()
        
        if existing_user:
            raise ValidationError('Username already exists')
```

In this example, the `validate_username` method is executed during form validation. It queries the database to check if a user with the same username already exists and raises a `ValidationError` if so.

## Conclusion

Handling form data and performing validation is a crucial part of web development. Flask-SQLAlchemy provides a convenient integration between Flask, SQLAlchemy, and Flask-WTF, making it easier to work with form data and databases in Flask applications.

In this blog post, we've covered setting up Flask-SQLAlchemy, creating a model, creating a form with Flask-WTF, and how to handle form data and perform validation.

This is just the tip of the iceberg when it comes to working with form data and databases in Flask-SQLAlchemy. For more advanced scenarios, make sure to refer to the Flask-SQLAlchemy and Flask-WTF documentation.

References:
- Flask-SQLAlchemy: [https://flask-sqlalchemy.palletsprojects.com/](https://flask-sqlalchemy.palletsprojects.com/)
- Flask-WTF: [https://flask-wtf.readthedocs.io/](https://flask-wtf.readthedocs.io/)
- WTForms: [https://wtforms.readthedocs.io/](https://wtforms.readthedocs.io/)
- SQLAlchemy: [https://www.sqlalchemy.org/](https://www.sqlalchemy.org/)