---
layout: post
title: "[python] Handling form data in Bottle using WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

When building web applications, handling form data is a common task. It's essential to validate the inputs received from users and perform necessary actions based on the data. In this blog post, we'll explore how to handle form data in [Bottle](https://bottlepy.org/), a lightweight web framework for Python, using [WTForms](https://wtforms.readthedocs.io/), a flexible form validation and rendering library.

## Table of Contents

- [Why use WTForms?](#why-use-wtforms)
- [Setting up the environment](#setting-up-the-environment)
- [Creating a simple form](#creating-a-simple-form)
- [Submitting and validating the form](#submitting-and-validating-the-form)
- [Handling form data](#handling-form-data)
- [Conclusion](#conclusion)

## Why use WTForms?

WTForms provides a simple and expressive way to define and validate forms in Python. It ensures that the data provided by users is in the expected format and meets the required criteria before processing it further. By using WTForms with Bottle, you can easily handle complex form validation and rendering tasks.

## Setting up the environment

Before we dive into using WTForms with Bottle, let's set up our environment by installing the required packages. We'll need both Bottle and WTForms, which can be installed using pip:

```python
pip install bottle
pip install wtforms
```

Additionally, ensure that you have a text editor or Integrated Development Environment (IDE) such as Visual Studio Code or PyCharm to write and run the code.

## Creating a simple form

To demonstrate handling form data with WTForms, let's create a simple contact form with two fields: name and email. First, create a new Python file, `app.py`, and import the necessary modules:

```python
from bottle import Bottle, request, template
from wtforms import Form, StringField, validators
```

Next, create a class for our form using WTForms:

```python
class ContactForm(Form):
    name = StringField('Name', validators=[validators.DataRequired()])
    email = StringField('Email', validators=[validators.DataRequired(), validators.Email()])
```

In the `ContactForm` class, we define two fields: `name` and `email`. We add validators to enforce that both fields are required, and the email field should be in a valid email format.

## Submitting and validating the form

Now that we have created our form, let's set up the route for the form submission. In the Bottle framework, routes are defined using the `@app.route()` decorator. Add the following code to your `app.py` file:

```python
app = Bottle()

@app.route('/contact', method='GET')
def show_contact_form():
    form = ContactForm()
    return template('contact_form', form=form)

@app.route('/contact', method='POST')
def process_contact_form():
    form = ContactForm(request.POST)
    if form.validate():
        # Handle the form data
        return "Form submitted successfully!"
    else:
        return template('contact_form', form=form)
```

In the `show_contact_form` function, we create an instance of the `ContactForm` class and pass it to the template `contact_form.tpl`. This template will render the form fields and any validation errors. We use the `GET` method to display the form initially.

In the `process_contact_form` function, we create another instance of the `ContactForm` class, this time passing the `request.POST` object containing the form data. We then validate the form using the `form.validate()` method. If the validation passes, we can proceed with handling the form data. Otherwise, we render the form template again, showing the validation errors.

## Handling form data

Once the form data is validated, you can access the values entered by users using the form field names. For example, to retrieve the name and email values in the `process_contact_form` function:

```python
name = form.name.data
email = form.email.data
```

You can then perform any necessary actions with the form data, such as saving it to a database, sending an email, or displaying a success message to the user.

## Conclusion

In this blog post, we explored how to handle form data in Bottle using WTForms. By utilizing the powerful features of WTForms, you can easily validate and process user inputs in your web applications. Remember to install the necessary dependencies, define your form using the WTForms library, and handle the form data based on your application's requirements. Happy coding!