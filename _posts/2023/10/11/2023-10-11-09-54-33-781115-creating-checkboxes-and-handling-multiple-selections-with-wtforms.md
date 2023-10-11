---
layout: post
title: "[python] Creating checkboxes and handling multiple selections with WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

When building web forms, it's common to include checkboxes to allow users to make multiple selections. In Python, one popular library for creating and validating web forms is **WTForms**. In this tutorial, we'll explore how to create checkbox fields and handle multiple selections using WTForms.

## Table of Contents
- [Getting Started with WTForms](#getting-started-with-wtforms)
- [Creating Checkbox Fields](#creating-checkbox-fields)
- [Handling Multiple Selections](#handling-multiple-selections)
- [Conclusion](#conclusion)

## Getting Started with WTForms

First, let's assume you have a basic Flask application with WTForms installed. If you haven't set up your project yet, you can follow the official Flask documentation to get started.

To use WTForms, you'll need to import the necessary modules:

```python
from flask_wtf import FlaskForm
from wtforms import SelectMultipleField, SubmitField
from wtforms.validators import DataRequired
```

## Creating Checkbox Fields

To create a checkbox field in WTForms, you'll need to use the `SelectMultipleField` class. This class allows users to select multiple options from a given list.

Here's an example of how to create a simple checkbox field with three options:

```python
class MyForm(FlaskForm):
    choices = [('option1', 'Option 1'), ('option2', 'Option 2'), ('option3', 'Option 3')]
    checkboxes = SelectMultipleField('Checkboxes', choices=choices, validators=[DataRequired()])
    submit = SubmitField('Submit')
```

In this example, we defined a `SelectMultipleField` named `checkboxes` with three checkbox options. We also added the `DataRequired` validator to ensure that at least one checkbox is selected.

## Handling Multiple Selections

To handle the user's selections, you can access the `data` attribute of the checkbox field in your Flask route. This attribute provides a list of the selected options.

```python
@app.route('/submit', methods=['GET', 'POST'])
def submit():
    form = MyForm()
    if form.validate_on_submit():
        selected_options = form.checkboxes.data
        # Process the selected options here
        return redirect('/')
    return render_template('form.html', form=form)
```

In this example, we define a Flask route `/submit` and retrieve the selected options from `form.checkboxes.data`. You can then process the selected options as needed and redirect the user to another page.

## Conclusion

In this tutorial, we explored how to create checkbox fields and handle multiple selections using WTForms. With WTForms, creating and validating web forms in Python becomes a breeze. By following this guide, you should be able to integrate checkbox fields successfully into your web forms and handle multiple selections with ease. Happy coding!