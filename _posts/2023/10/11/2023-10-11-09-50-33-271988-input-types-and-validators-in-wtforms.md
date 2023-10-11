---
layout: post
title: "[python] Input types and validators in WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

When building web applications, one common task is to handle user input and validate it before processing. WTForms is a powerful form validation library in Python that makes this process easier and more efficient. In this blog post, we will explore the various input types and validators available in WTForms.

## Input Types

WTForms provides several input types that you can use in your forms. These input types help you define the type of data expected from the user. Let's take a look at some commonly used input types:

### StringField

The StringField is the most basic input type in WTForms. It represents a text input field and is used to capture strings from the user. It can be created with the following code:

```python
from wtforms import StringField

my_field = StringField('My Field')
```

### IntegerField

The IntegerField is used to capture integer values from the user. It validates that the input is a whole number. It can be created as follows:

```python
from wtforms import IntegerField

my_field = IntegerField('My Field')
```

### BooleanField

The BooleanField is used to capture boolean values from the user. It represents a checkbox input. It can be created with the following code:

```python
from wtforms import BooleanField

my_field = BooleanField('My Field')
```

### DateField

The DateField is used to capture dates from the user. It validates that the input is a valid date. It can be created as follows:

```python
from wtforms import DateField

my_field = DateField('My Field')
```

### SelectField

The SelectField is used to capture choices from the user. It can be used to create drop-down menus or select boxes. It can be created with the following code:

```python
from wtforms import SelectField

my_field = SelectField('My Field', choices=[('option1', 'Option 1'), ('option2', 'Option 2')])
```

## Validators

WTForms also provides a wide range of validators that you can use to validate user input. Validators are used to ensure that the input meets certain criteria or constraints. Let's take a look at some commonly used validators:

### Data Required Validator

The Data Required validator is used to ensure that the input is not empty. It can be used as follows:

```python
from wtforms.validators import DataRequired

my_field = StringField('My Field', validators=[DataRequired()])
```

### Length Validator

The Length validator is used to validate the length of input data. It ensures that the input is within a specified range. It can be used as follows:

```python
from wtforms.validators import Length

my_field = StringField('My Field', validators=[Length(min=2, max=20)])
```

### Email Validator

The Email validator is used to validate email addresses. It checks if the input follows the correct email format. It can be used as follows:

```python
from wtforms.validators import Email

my_field = StringField('My Field', validators=[Email()])
```

### Custom Validators

WTForms also allows you to create custom validators to enforce your own validation rules. You can create custom validators by subclassing the `Validator` class and implementing the `__call__` method. Here's an example:

```python
from wtforms.validators import ValidationError

class MyCustomValidator:
    def __call__(self, form, field):
        if field.data != 'my_custom_value':
            raise ValidationError('Invalid input.')
            
my_field = StringField('My Field', validators=[MyCustomValidator()])
```

By combining input types and validators, you can create powerful and flexible forms using WTForms. It provides a solid foundation for handling user input and ensuring data integrity in your web applications.

In this blog post, we explored some of the commonly used input types and validators in WTForms. However, WTForms offers many more input types and validators that you can explore in their official documentation.