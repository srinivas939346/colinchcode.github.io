---
layout: post
title: "[python] Creating dynamic forms with WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

In web development, creating forms is a common task. These forms often need to be dynamically generated based on various conditions or user input. `WTForms` is a popular Python library that makes form creation and validation easy and straightforward. In this blog post, we will explore how to create dynamic forms using `WTForms`.

## Table of Contents
1. [Introduction to WTForms](#introduction-to-wtforms)
2. [Creating a basic form](#creating-a-basic-form)
3. [Adding dynamic fields](#adding-dynamic-fields)
4. [Updating form based on user input](#updating-form-based-on-user-input)
5. [Conclusion](#conclusion)

## Introduction to WTForms <a name="introduction-to-wtforms"></a>
`WTForms` is a flexible forms validation and rendering library for Python web development frameworks like Flask, Django, and more. It provides a simple and intuitive way to define forms and handle form validation.

## Creating a basic form <a name="creating-a-basic-form"></a>
To get started, let's create a basic form using `WTForms`. We'll create a simple form with two fields: name and email.

First, let's install `WTForms`:

```bash
pip install wtforms
```

Now, create a file named `forms.py` and add the following code:

```python
from wtforms import Form, StringField

class MyForm(Form):
    name = StringField('Name')
    email = StringField('Email')
```

In the above code, we imported the necessary classes from `WTForms` and created a class `MyForm` that inherits from `Form`. We added two fields to the form: `name` and `email`, both of which are instances of the `StringField` class.

## Adding dynamic fields <a name="adding-dynamic-fields"></a>
One of the powerful features of `WTForms` is the ability to generate fields dynamically. Let's say we want to create a form where users can input their skills. The number of skills can vary, so we need a way to dynamically add fields.

```python
from wtforms import FieldList, FormField, StringField

class SkillForm(Form):
    skill = StringField('Skill')

class MyForm(Form):
    name = StringField('Name')
    email = StringField('Email')
    skills = FieldList(FormField(SkillForm))
```

In the above code, we created a separate `SkillForm` class which represents a single skill input field. Then, we added a `FieldList` of `SkillForm` instances to the main `MyForm` class. This allows us to dynamically add or remove skill input fields.

## Updating form based on user input <a name="updating-form-based-on-user-input"></a>
`WTForms` also allows us to update the form fields dynamically based on user input. Let's say we have a form where users can select their country, and based on the selected country, we want to display additional fields.

```python
from wtforms import Form, SelectField, StringField, validators

class CountryForm(Form):
    country = SelectField('Country', choices=[('us', 'United States'), ('ca', 'Canada')])

class MyForm(Form):
    name = StringField('Name')
    email = StringField('Email')
    country = FormField(CountryForm)

    def validate_country(self, field):
        if field.data == 'us':
            self.city = StringField('City')
            self.state = StringField('State')
        elif field.data == 'ca':
            self.province = StringField('Province')
```

In the above code, we created a separate `CountryForm` class which represents the country selection field. We added a `country` field to the main `MyForm` class, which is an instance of `CountryForm`. We also added a custom validation method `validate_country` which gets triggered when the form is submitted. Inside this method, we update the form dynamically based on the selected country.

## Conclusion <a name="conclusion"></a>
`WTForms` is a powerful library for creating dynamic forms in Python web development. It provides an easy way to define forms and handle form validation. In this blog post, we explored the basics of using `WTForms` and creating dynamic forms with dynamically generated fields based on user input. This is just the tip of the iceberg, and `WTForms` offers many more features to make form creation a breeze.