---
layout: post
title: "[python] Creating form wizards with WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

**WTForms** is a powerful and flexible form library for Python that can be used to create form wizards. Form wizards allow you to break down a complex form into multiple steps or pages, making it easier for users to fill out long forms.

In this tutorial, we will walk through the process of creating a form wizard using WTForms. We will use the Flask web framework to create a simple web application to demonstrate how the form wizard works.

## Table of Contents

- [Setting Up the Environment](#setting-up-the-environment)
- [Creating the Form Classes](#creating-the-form-classes)
- [Creating the Flask Application](#creating-the-flask-application)
- [Creating the Form Wizard](#creating-the-form-wizard)
- [Handling Form Submission](#handling-form-submission)
- [Conclusion](#conclusion)

## Setting Up the Environment

To get started, you should have Python and Flask installed on your machine. You can install Flask using pip with the following command:

```python
pip install flask
```

Next, create a new directory for our project and navigate to that directory in your terminal.

## Creating the Form Classes

WTForms allows us to define our form fields and validation rules as Python classes. In our case, we will create three separate form classes, each representing a step in our form wizard.

Let's create a new file called `forms.py` and define our form classes:

```python
from wtforms import Form, StringField, IntegerField
from wtforms.validators import DataRequired, Length, NumberRange

class Step1Form(Form):
    name = StringField('Name', validators=[DataRequired(), Length(max=50)])

class Step2Form(Form):
    age = IntegerField('Age', validators=[DataRequired(), NumberRange(min=18, max=100)])

class Step3Form(Form):
    email = StringField('Email', validators=[DataRequired(), Length(max=100)])
```

In this example, we have created three form classes for three steps. Each form class contains the fields required for that step, along with the necessary validators.

## Creating the Flask Application

Create a new file called `app.py` and add the following code to set up a basic Flask application:

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

if __name__ == '__main__':
    app.run(debug=True)
```

## Creating the Form Wizard

Now let's create the form wizard itself. We will use Flask's `render_template` function to render the appropriate form for each step.

```python
from flask import Flask, render_template
from flask_wtf import FlaskForm
from wtforms import StringField, IntegerField, SubmitField
from wtforms.validators import DataRequired, Length, NumberRange
from flask_wtf.wizards import Wizard

app = Flask(__name__)
app.config['SECRET_KEY'] = 'your-secret-key'

class Step1Form(FlaskForm):
    name = StringField('Name', validators=[DataRequired(), Length(max=50)])
    next_step = SubmitField('Next')

class Step2Form(FlaskForm):
    age = IntegerField('Age', validators=[DataRequired(), NumberRange(min=18, max=100)])
    previous_step = SubmitField('Previous')
    next_step = SubmitField('Next')

class Step3Form(FlaskForm):
    email = StringField('Email', validators=[DataRequired(), Length(max=100)])
    previous_step = SubmitField('Previous')
    submit = SubmitField('Submit')

class MyWizard(Wizard):
    steps = [('step1', Step1Form), ('step2', Step2Form), ('step3', Step3Form)]


@app.route('/', methods=['GET', 'POST'])
def index():
    wizard = MyWizard(formdata=None)
    wizard.add_step(Step1Form)
    wizard.add_step(Step2Form)
    wizard.add_step(Step3Form)
    
    if wizard.validate_on_submit():
        # Process the form data
        return render_template('success.html')
    
    return render_template('wizard.html', form=wizard)

if __name__ == '__main__':
    app.run(debug=True)
```

Here, we define three form classes for each step, along with the necessary submit buttons to navigate between the steps. We also define a `MyWizard` class that inherits from Flask's `Wizard` class and specifies the order of the steps.

In the `index` route, we create an instance of our wizard and add the steps. If the form is valid, we can process the form data and render a success page. Otherwise, we render the wizard template along with the current form.

## Handling Form Submission

To handle form submission in the last step, we can add a new route that accepts a `POST` request and processes the form data.

```python
@app.route('/submit', methods=['POST'])
def submit():
    # Process the form data
    return render_template('success.html')
```

In this example, we simply return a success page when the form is submitted.

## Conclusion

In this tutorial, we learned how to create a form wizard using WTForms and Flask. We defined separate form classes for each step and used Flask's `render_template` function to render the appropriate form for each step. We also saw how to handle form submission and process the form data.

Form wizards are a great way to improve the user experience when dealing with long or complex forms. With WTForms, creating form wizards becomes a breeze, allowing you to easily break down the form into manageable steps.