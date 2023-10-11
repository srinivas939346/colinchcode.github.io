---
layout: post
title: "[python] Handling form submissions in Flask using WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

When building web applications with Flask, handling form submissions is an essential task. While you can manually work with form data in Flask, using a form validation and rendering library like WTForms can make the process much easier and more organized.

In this tutorial, we will go through the steps of setting up and handling form submissions using WTForms in Flask.

## Table of Contents
- [Installation](#installation)
- [Creating a Form](#creating-a-form)
- [Rendering the Form](#rendering-the-form)
- [Handling Form Submissions](#handling-form-submissions)
- [Conclusion](#conclusion)

## Installation

First, let's install WTForms using pip:

```bash
pip install wtforms
```

Once installed, you're ready to create and work with forms in your Flask application.

## Creating a Form

To create a form using WTForms, you'll typically define a class that represents the form fields. This class will inherit from the `flask_wtf.FlaskForm` class provided by WTForms.

Let's create a simple form that takes a name and email as inputs:

```python
from flask_wtf import FlaskForm
from wtforms import StringField, SubmitField
from wtforms.validators import DataRequired, Email

class MyForm(FlaskForm):
    name = StringField('Name', validators=[DataRequired()])
    email = StringField('Email', validators=[DataRequired(), Email()])
    submit = SubmitField('Submit')
```

In this example, we have defined two fields: `name` and `email` using `StringField` from WTForms. We have also added some validators to ensure the fields are not empty and the email is in a valid format.

## Rendering the Form

To render the form in a view, you'll need to pass an instance of the form class to the template.

```python
from flask import Flask, render_template
from forms import MyForm

app = Flask(__name__)
app.config['SECRET_KEY'] = 'your_secret_key_here'

@app.route('/form', methods=['GET', 'POST'])
def form():
    my_form = MyForm()
    return render_template('form.html', form=my_form)
```

In the above example, we import the form class from the `forms.py` file and pass an instance of the form (`my_form`) to the `form.html` template.

In the `form.html` template, you can use WTForms' template rendering helpers to render the form fields:

```jinja2
<form method="POST" action="{{ url_for('form') }}">
    {{ form.csrf_token }}
    
    {{ form.name.label }}
    {{ form.name() }}
    
    {{ form.email.label }}
    {{ form.email() }}
    
    {{ form.submit() }}
</form>
```

The `{{ form.csrf_token }}` is a security feature provided by WTForms to protect against CSRF attacks.

## Handling Form Submissions

To handle form submissions, you'll need to check if the request method is `POST`, and then validate and process the form data.

```python
from flask import Flask, redirect, url_for, render_template
from forms import MyForm

app = Flask(__name__)
app.config['SECRET_KEY'] = 'your_secret_key_here'

@app.route('/form', methods=['GET', 'POST'])
def form():
    my_form = MyForm()
    
    if my_form.validate_on_submit():
        # Process form data
        name = my_form.name.data
        email = my_form.email.data
        
        # Redirect to a success page
        return redirect(url_for('success'))
    
    return render_template('form.html', form=my_form)

@app.route('/success')
def success():
    return 'Form submitted successfully!'

if __name__ == '__main__':
    app.run()
```

In the above example, when the form is submitted, the `validate_on_submit()` method is called to validate the form data. If the form data is valid, you can access the data through the form fields' `data` attribute.

If the form is not valid, the form will be re-rendered with the validation errors.

## Conclusion

In this tutorial, we have seen how to handle form submissions in Flask using WTForms. With WTForms, you can easily create forms, validate form data, and process form submissions. This improves the overall user experience and helps keep your code organized.