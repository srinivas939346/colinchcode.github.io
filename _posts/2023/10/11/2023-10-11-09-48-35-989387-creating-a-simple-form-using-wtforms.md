---
layout: post
title: "[python] Creating a simple form using WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

In this tutorial, we will learn how to create a simple form using WTForms, a powerful form handling library for Python. 

## Table of Contents
- [Introduction to WTForms](#introduction-to-wtforms)
- [Setting Up a Flask App](#setting-up-a-flask-app)
- [Creating a Form Class](#creating-a-form-class)
- [Displaying the Form](#displaying-the-form)
- [Handling Form Submission](#handling-form-submission)

## Introduction to WTForms

WTForms is a flexible and feature-rich library that simplifies the process of creating and handling HTML forms in Python web applications. It provides a simple and declarative syntax for defining forms, handling form validation, and rendering form fields.

To get started, we need to have WTForms installed in our project. You can install it via pip:

```python
pip install WTForms
```

## Setting Up a Flask App

First, let's set up a basic Flask application. Create a new directory for your project and navigate to it in your terminal. Then, create a virtual environment and activate it:

```python
python -m venv myenv
source myenv/bin/activate (for macOS/Linux) or myenv\Scripts\activate (for Windows)
```

Next, install Flask:

```python
pip install Flask
```

Create a new file named `app.py` and add the following code to set up a basic Flask app:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return 'Hello, Flask!'

if __name__ == '__main__':
    app.run()
```

You can run your Flask app by executing `python app.py` in your terminal and visiting `http://localhost:5000` in your browser. You should see the "Hello, Flask!" message.

## Creating a Form Class

Now, let's create a form using WTForms. In your `app.py`, import the necessary modules:

```python
from flask import Flask, render_template
from flask_wtf import FlaskForm
from wtforms import StringField, SubmitField
```

Next, define a form class by subclassing `FlaskForm`:

```python
class MyForm(FlaskForm):
    name = StringField('Name')
    email = StringField('Email')
    submit = SubmitField('Submit')
```

In the `MyForm` class, we defined two form fields: `name` and `email` of type `StringField`, and a submit button field of type `SubmitField`. 

## Displaying the Form

To render and display the form in a template, create a new template file named `index.html` in a `templates` directory. Add the following code to the `index.html` file:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Simple Form Example</title>
</head>
<body>
    <h1>Simple Form Example</h1>
    <form method="POST" action="">
        {{ form.hidden_tag() }}
        <div>
            {{ form.name.label }}
            {{ form.name() }}
        </div>
        <div>
            {{ form.email.label }}
            {{ form.email() }}
        </div>
        <div>
            {{ form.submit() }}
        </div>
    </form>
</body>
</html>
```

In the `index.html` template, we use the `form` object to render the form fields and labels. The `hidden_tag()` method is used to render a hidden field required for CSRF protection.

## Handling Form Submission

To handle form submission, we'll modify the `index` route in the `app.py` file:

```python
from flask import Flask, render_template, request

@app.route('/', methods=['GET', 'POST'])
def index():
    form = MyForm()
    if form.validate_on_submit():
        name = form.name.data
        email = form.email.data
        # Process the form data
        return f"Thank you, {name}! Your email ({email}) has been registered."
    return render_template('index.html', form=form)
```

In the modified `index` route, we instantiate the `MyForm` class. If the form is submitted and passes the form validation, we retrieve the data entered by the user and process it accordingly.

That's it! You have successfully created a simple form using WTForms. Run your Flask app and visit `http://localhost:5000` to see the form in action.

Now you can build more complex forms with validation, custom validators, and other advanced features provided by WTForms to enhance the user experience of your web application.

Feel free to explore the [WTForms documentation](https://wtforms.readthedocs.io/) for more information about its capabilities and usage.