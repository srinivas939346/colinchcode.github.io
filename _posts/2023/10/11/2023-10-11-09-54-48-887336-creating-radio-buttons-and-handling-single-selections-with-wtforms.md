---
layout: post
title: "[python] Creating radio buttons and handling single selections with WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to create radio buttons in a form using the WTForms library in Python. Radio buttons are commonly used to allow users to select only one option from a group of choices. WTForms provides an easy and efficient way to handle radio buttons and their selections.

## Table of Contents
- [Introduction](#introduction)
- [Setting up the Project](#setting-up-the-project)
- [Creating the Form](#creating-the-form)
- [Handling User Selections](#handling-user-selections)
- [Conclusion](#conclusion)

## Introduction

WTForms is a flexible forms validation and rendering library for Python web development. It provides a simple way to define and handle forms in a Pythonic way. WTForms supports various field types, including radio buttons, which we will focus on in this tutorial.

## Setting up the Project

Before we proceed, let's make sure we have WTForms installed. You can install it using pip:

```shell
pip install wtforms
```

Now that we have WTForms installed, let's create a new Python file for our project.

```python
# radio_buttons_example.py
from flask import Flask, render_template
from flask_wtf import FlaskForm
from wtforms import RadioField, SubmitField

app = Flask(__name__)
app.config['SECRET_KEY'] = 'secret_key'

# Your code goes here

if __name__ == '__main__':
    app.run()
```

## Creating the Form

To create a form with radio buttons, we need to define a class that inherits from `FlaskForm` and add a `RadioField` to it.

```python
class RadioForm(FlaskForm):
    options = RadioField('Options', choices=[('option1', 'Option 1'), ('option2', 'Option 2'), ('option3', 'Option 3')])
    submit = SubmitField('Submit')
```

In the example above, we have created a `RadioForm` class that has a `RadioField` named `options`. The `choices` parameter is a list of tuples, where the first element of each tuple is the value to be returned when the radio button is selected, and the second element is the label to be displayed.

## Handling User Selections

To handle user selections from the radio buttons, we can use the `validate_on_submit()` method provided by WTForms. In the route where we render the form, we can check if the form has been submitted and validate it.

```python
@app.route('/', methods=['GET', 'POST'])
def index():
    form = RadioForm()
    if form.validate_on_submit():
        selected_option = form.options.data
        # Your code to handle the selected option goes here
    return render_template('index.html', form=form)
```

Inside the `index()` route, we create an instance of `RadioForm()`. We then check if the form has been submitted by calling `form.validate_on_submit()`. If the form is valid, we can access the selected option using `form.options.data`.

## Conclusion

In this blog post, we explored how to create radio buttons and handle single selections using WTForms in Python. WTForms provides an easy-to-use and efficient way to define and handle forms. With WTForms, you can create user-friendly forms with radio buttons and handle the selections seamlessly.

Remember to install WTForms using pip before running the code. Feel free to experiment with the code and customize it to fit your specific needs. Happy coding!