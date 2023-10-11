---
layout: post
title: "[python] Displaying form data in Flask using WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

Flask is a web framework for Python that allows you to build web applications. WTForms is a form handling library that simplifies the process of creating and validating HTML forms in Flask.

In this tutorial, we will learn how to use WTForms to display form data in Flask. We will assume that you already have a basic understanding of Flask and have it installed in your development environment.

## Table of Contents
1. [Installing WTForms](#installing-wtforms)
2. [Creating a Form](#creating-a-form)
3. [Displaying the Form](#displaying-the-form)
4. [Processing Form Data](#processing-form-data)
5. [Conclusion](#conclusion)

## 1. Installing WTForms <a name="installing-wtforms"></a>

To start using WTForms in your Flask project, you need to install it first. You can install WTForms using pip by running the following command in your terminal:

```shell
pip install WTForms
```

## 2. Creating a Form <a name="creating-a-form"></a>

Let's begin by creating a simple form using WTForms. In your Flask project, create a new Python file called `forms.py` and add the following code:

```python
from flask_wtf import FlaskForm
from wtforms import StringField, SubmitField

class MyForm(FlaskForm):
    name = StringField('Name')
    submit = SubmitField('Submit')
```

In the above code, we import the necessary classes from WTForms. We then create a `MyForm` class that inherits from `FlaskForm`. Inside this class, we define form fields such as `name` of type `StringField` and `submit` of type `SubmitField`.

## 3. Displaying the Form <a name="displaying-the-form"></a>

Next, let's create a route in your Flask application to display the form. In one of your views, import the `MyForm` class from `forms.py` and add the following code:

```python
from flask import render_template
from forms import MyForm

@app.route('/form', methods=['GET', 'POST'])
def form():
    form = MyForm()
    return render_template('form.html', form=form)
```

In the above code, we create an instance of `MyForm` and pass it to the template rendering function `render_template`. This will make the form available to the template.

## 4. Processing Form Data <a name="processing-form-data"></a>

To process the form data submitted by the user, we need to modify the `form` route in your Flask application. Add the following code to the existing `form` route:

```python
@app.route('/form', methods=['GET', 'POST'])
def form():
    form = MyForm()
    if form.validate_on_submit():
        name = form.name.data
        # Process the form data here
        return 'Form submitted successfully'
    return render_template('form.html', form=form)
```

In the above code, we check if the form data is valid using the `validate_on_submit` method of the form. If it is valid, we can access the form data using the `data` attribute of each form field. You can then process the form data according to your application's requirements.

## 5. Conclusion <a name="conclusion"></a>

In this tutorial, we learned how to use WTForms to display form data in Flask. We covered the installation of WTForms, creating a form using WTForms, displaying the form in a Flask view, and processing the form data. WTForms provides a convenient way to handle form data in Flask applications and makes it easy to incorporate form validation.

You can find more information and examples on how to use WTForms in the [official documentation](https://wtforms.readthedocs.io/).