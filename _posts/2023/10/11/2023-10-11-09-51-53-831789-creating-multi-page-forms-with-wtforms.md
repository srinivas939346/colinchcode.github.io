---
layout: post
title: "[python] Creating multi-page forms with WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

In web development, forms are a crucial component for capturing user input. Sometimes, complex forms with multiple sections or pages are required to gather extensive information. In this blog post, we will explore how to create multi-page forms using WTForms, a popular form library in Python.

## Table of Contents
- [What is WTForms?](#what-is-wtforms)
- [Setting up WTForms](#setting-up-wtforms)
- [Creating the Form](#creating-the-form)
- [Splitting the Form into Pages](#splitting-the-form-into-pages)
- [Handling Form Submissions](#handling-form-submissions)
- [Conclusion](#conclusion)

## What is WTForms?
WTForms is a flexible form library for Python web development frameworks like Flask, Django, and Pyramid. It provides easy-to-use form handling and validation functionality, making it a popular choice among developers.

## Setting up WTForms
Before we dive into creating multi-page forms, let's set up WTForms in our Python environment. Start by installing it via pip:

```bash
pip install WTForms
```

Once installed, you can import it into your Python script or web application:

```python
from wtforms import Form, StringField, SubmitField
from wtforms.validators import DataRequired, Email
```

## Creating the Form
To create a multi-page form, we need to define a WTForms class, similar to how we would create a regular form. Let's consider a simple example where we ask the user for their name and email address:

```python
class MyForm(Form):
    name = StringField('Name', validators=[DataRequired()])
    email = StringField('Email', validators=[DataRequired(), Email()])
    submit = SubmitField('Next')
```

In this example, we define two fields, `name` and `email`, along with their corresponding validators. We also include a `submit` button to proceed to the next page.

## Splitting the Form into Pages
To split our form into multiple pages, we need to implement a way to navigate between the pages. One approach is to use tabs or buttons to switch between form sections. 

Here's an example of how to split our form into two pages, with a "Next" button to navigate between them:

```python
class MyForm(Form):
    # fields for page 1
    name = StringField('Name', validators=[DataRequired()])
    submit_page1 = SubmitField('Next')

    # fields for page 2
    email = StringField('Email', validators=[DataRequired(), Email()])
    submit_page2 = SubmitField('Submit')

# In your view function or endpoint:
@app.route('/form', methods=['GET', 'POST'])
def form():
    form = MyForm()
    
    if form.validate_on_submit():
        if form.submit_page1.data:
            # handle page 1 form submission
            # redirect to page 2
        elif form.submit_page2.data:
            # handle page 2 form submission
            # process the complete form
            # redirect to success page
            
    return render_template('form.html', form=form)
```

By checking which submit button is clicked, we can handle the form data differently for each page. After processing the complete form, we can redirect the user to the desired page.

## Handling Form Submissions
Once the user has completed all the form pages, we need to handle the final submission and process the complete form. Depending on your web framework, you might store the form data in a database, send emails, or perform other actions.

After processing the complete form, don't forget to redirect the user to an appropriate success page or thank you message.

## Conclusion
In this blog post, we explored how to create multi-page forms using WTForms in Python. WTForms provides an intuitive way to handle form validation and data submission. With a few modifications and logic, we can split our forms into multiple pages, providing an organized and user-friendly form experience.