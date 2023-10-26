---
layout: post
title: "[python] Using Flask-WTForms with SQLAlchemy for form handling"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In web development, handling forms is a common task. Flask, a popular web framework in Python, provides an extension called Flask-WTForms that makes form handling easy and efficient. In combination with SQLAlchemy, a powerful Object-Relational Mapping (ORM) library, you can seamlessly integrate form processing and data persistence in your Flask application.

## Prerequisites

Make sure you have Flask and SQLAlchemy installed in your Python environment. If not, you can install them using pip:

```python
pip install Flask SQLAlchemy
```

Also, install Flask-WTForms:

```python
pip install Flask-WTF
```

## Steps to Follow

1. Create a Flask application:

```python
from flask import Flask, render_template, redirect, url_for
from flask_wtf import FlaskForm
from wtforms import StringField, SubmitField
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///form_data.db'  # change the database URL as per your requirement
app.config['SECRET_KEY'] = 'your_secret_key'
db = SQLAlchemy(app)
```

2. Define the form class using Flask-WTForms:

```python
class MyForm(FlaskForm):
    name = StringField('Name')
    email = StringField('Email')
    submit = SubmitField('Submit')
```

3. Create the database model using SQLAlchemy:

```python
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(100))
    email = db.Column(db.String(100))
```

4. Define a route to handle form submission:

```python
@app.route('/', methods=['GET', 'POST'])
def index():
    form = MyForm()
    if form.validate_on_submit():
        user = User(name=form.name.data, email=form.email.data)
        db.session.add(user)
        db.session.commit()
        return redirect(url_for('index'))
    return render_template('index.html', form=form)
```

5. Create a template to display the form:

```python
{% raw %}
{% extends 'base.html' %}

{% block content %}
<form method="POST" action="{{ url_for('index') }}">
    {{ form.hidden_tag() }}
    {{ form.name.label }} {{ form.name }}
    {{ form.email.label }} {{ form.email }}
    {{ form.submit }}
</form>
{% endblock %}
{% endraw %}
```

6. Run the Flask application:

```python
if __name__ == '__main__':
    app.run(debug=True)
```

## Explanation

- In step 1, we import the necessary modules and create a Flask application instance. We also configure the SQLAlchemy database URL and set a secret key for CSRF protection.
- In step 2, we define a form class `MyForm` using Flask-WTForms. It has two fields: `name` and `email`, and a submit button.
- In step 3, we create the database model `User` using SQLAlchemy. It has `id`, `name`, and `email` fields.
- In step 4, we define a route `/` that handles both GET and POST requests. If the form is submitted and passes validation, we create a new `User` object and save it to the database using SQLAlchemy.
- In step 5, we create a template to render the form. We use `url_for` to specify the form submission URL and Flask-WTForms methods to generate the form fields.
- Finally, in step 6, we run the Flask application.

This is a basic example of using Flask-WTForms with SQLAlchemy for form handling in a Flask application. You can further customize it according to your requirements.