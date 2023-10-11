---
layout: post
title: "[python] Flattening nested dict inputs with WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

When working with web forms in Python, **WTForms** is a popular library for validating and handling form data. It provides a simple and intuitive way to define forms and validate user inputs. One common challenge is dealing with nested dictionary inputs, where the data is structured hierarchically. In this article, we'll explore how to flatten such nested dictionary inputs with WTForms.

## Understanding Nested Dictionary Inputs

Imagine we have a registration form that asks for the user's personal information, including their name, email, and address. The address information can itself be a nested dictionary, containing fields such as street, city, and country. The input data might look something like this:

```python
data = {
    "name": "John Doe",
    "email": "johndoe@example.com",
    "address": {
        "street": "123 Main St",
        "city": "Anytown",
        "country": "USA"
    }
}
```

## Creating a WTForms Form

To flatten the nested dictionary, we need to create a WTForms form that mirrors the structure of the input data. We'll define separate fields for each key in the input dictionary. In our example, we might create a `RegistrationForm` with fields like `name`, `email`, `address_street`, `address_city`, and `address_country`.

Here's how we can define the form using WTForms:

```python
from wtforms import Form, StringField

class RegistrationForm(Form):
    name = StringField("Name")
    email = StringField("Email")
    address_street = StringField("Street")
    address_city = StringField("City")
    address_country = StringField("Country")
```

## Flattening the Nested Dictionary Input

Now that we have our WTForms form, we can use it to validate and process the flattened data. To do this, we'll create an instance of the `RegistrationForm` class and populate it with the flattened dictionary values. We can then use the `validate()` method of the form to validate the user's inputs.

Here's an example of how we can flatten the nested dictionary and validate it with our form:

```python
def flatten_dict(data, prefix=''):
    flattened = {}
    for key, value in data.items():
        if isinstance(value, dict):
            flattened.update(flatten_dict(value, prefix + key + '_'))
        else:
            flattened[prefix + key] = value
    return flattened

def process_registration_form(data):
    form = RegistrationForm()
    flattened_data = flatten_dict(data)
    form.process(data=flattened_data)

    if form.validate():
        # Process the form data
        name = form.name.data
        email = form.email.data
        address_street = form.address_street.data
        address_city = form.address_city.data
        address_country = form.address_country.data

        # Additional processing...

        return True
    else:
        return False
```

In the above code snippet, we define a helper function `flatten_dict()` that iterates over the input dictionary and recursively flattens it by concatenating the nested keys with the parent key.

The `process_registration_form()` function takes the nested dictionary data, flattens it using `flatten_dict()`, and processes it with the `RegistrationForm`. If the form data is valid, we can access the flattened form fields like `form.address_street.data` to retrieve the user input.

## Conclusion

Handling nested dictionary inputs with WTForms can be made simple by properly flattening the data beforehand. By creating a WTForms form that mirrors the structure of the input dictionary and using a helper function to flatten the data, we can easily validate and process the user's inputs. WTForms provides a robust and flexible solution for working with web forms in Python, and with these techniques, you can handle complex nested inputs with ease.