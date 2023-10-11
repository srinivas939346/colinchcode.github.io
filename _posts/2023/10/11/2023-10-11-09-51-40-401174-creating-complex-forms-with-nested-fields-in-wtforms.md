---
layout: post
title: "[python] Creating complex forms with nested fields in WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

When it comes to developing web applications, creating forms is an essential part of the process. WTForms is a powerful form library for Python that makes it easy to handle form validation, rendering, and data processing. In this tutorial, we'll explore how to create complex forms with nested fields using WTForms.

## Table of Contents

1. [Introduction to WTForms](#introduction-to-wtforms)
2. [Creating a basic WTForms form](#creating-a-basic-wtforms-form)
3. [Adding nested fields](#adding-nested-fields)
4. [Validating nested fields](#validating-nested-fields)
5. [Rendering nested fields](#rendering-nested-fields)
6. [Conclusion](#conclusion)

## Introduction to WTForms

WTForms provides a simple and flexible way to define and validate forms in Python. It allows you to define fields, add validators, and handle form data effortlessly. To get started, you'll need to install WTForms using `pip`.

```python
pip install WTForms
```

Once installed, you can import the necessary classes and methods from `wtforms` to start working with forms.

## Creating a basic WTForms form

Before diving into nested fields, let's first create a basic form using WTForms. We'll create a simple registration form with two fields: name and email.

```python
from wtforms import Form, StringField, EmailField

class RegistrationForm(Form):
    name = StringField("Name")
    email = EmailField("Email")
```

In the above code, `RegistrationForm` is a subclass of `Form` that defines the structure of our form. We define two fields - `name` and `email` - using the `StringField` and `EmailField` classes respectively.

## Adding nested fields

To create a form with nested fields, we can leverage the `FieldList` class provided by WTForms. This allows us to define a list of repeated fields within our form.

Let's modify our `RegistrationForm` to include a list of phone numbers:

```python
from wtforms import Form, StringField, EmailField, FieldList, FormField

class PhoneNumberForm(Form):
    number = StringField("Phone Number")
    # Add additional fields like country code, label, etc. if needed
    
class RegistrationForm(Form):
    name = StringField("Name")
    email = EmailField("Email")
    phone_numbers = FieldList(FormField(PhoneNumberForm), min_entries=1)
```

In the code above, we created a new form class `PhoneNumberForm` that represents a single phone number field. Then, we added a `FieldList` called `phone_numbers` to the `RegistrationForm`, specifying that it contains instances of the `PhoneNumberForm`. The `min_entries` argument ensures that at least one phone number is required.

## Validating nested fields

WTForms provides built-in validators that can be applied to form fields for validation purposes. To validate nested fields, we can define validators for each nested field or use the `validates` decorator to define a validation method for the containing form.

Let's add a validator to the `PhoneNumberForm` to ensure that the phone number is in a valid format:

```python
from wtforms.validators import Regexp

class PhoneNumberForm(Form):
    number = StringField("Phone Number", validators=[Regexp(r'^[0-9]{10}$', message='Invalid phone number format')])
```

In the code above, we applied the `Regexp` validator to the `number` field to ensure that it matches the specified regular expression pattern. You can add more validators as per your requirements.

## Rendering nested fields

{% raw %}
To render nested fields in your HTML template, you can use the `{{ form.field_name }}` notation provided by WTForms. You can also iterate over lists of fields using `{% for field in form.field_name %}`.
{% endraw %}
Here's an example HTML snippet for rendering the nested `phone_numbers` field:

```html
{% raw %}
{% for phone in form.phone_numbers %}
    <div class="form-group">
        {{ phone.number.label }}: {{ phone.number }}
    </div>
{% endfor %}
{% endraw %}
```

In the code above, we iterate over the `phone_numbers` field and render each phone number field with its label.

## Conclusion

By leveraging the power of WTForms, you can easily create complex forms with nested fields in your Python web applications. Whether it's a registration form, a survey form, or any other form requiring nested fields, WTForms provides a flexible and efficient solution. Experiment with different field types, validation rules, and rendering options to suit your specific needs. Happy coding!