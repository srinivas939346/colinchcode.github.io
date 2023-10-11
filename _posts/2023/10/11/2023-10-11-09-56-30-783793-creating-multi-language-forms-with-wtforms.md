---
layout: post
title: "[python] Creating multi-language forms with WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

In today's globalized world, it's crucial to provide users with the ability to interact with your applications or websites in their preferred language. When it comes to building forms, a popular library to work with in Python is WTForms. 

WTForms provides a simple and flexible way to define and validate forms in Python. In this article, we'll explore how to create multi-language forms using WTForms, allowing users to input data in different languages.

## Table of Contents
- [Setting up WTForms](#setting-up-wtforms)
- [Creating a Multi-Language Form](#creating-a-multi-language-form)
- [Translating Form Labels](#translating-form-labels)
- [Handling Form Validation Messages](#handling-form-validation-messages)
- [Switching Between Languages](#switching-between-languages)
- [Conclusion](#conclusion)

## Setting up WTForms
Before we dive into multi-language forms, let's make sure we have WTForms installed in our project. You can install it using pip:

```python
pip install WTForms
```

## Creating a Multi-Language Form
To start building our multi-language form, we need to define the necessary forms using WTForms. Here's an example of a simple form that includes a few fields:

```python
from wtforms import Form, StringField, SubmitField

class MyForm(Form):
    name = StringField('Name')
    email = StringField('Email')
    submit = SubmitField('Submit')
```

## Translating Form Labels
To make our form multi-language, we need to introduce translations for the form labels. One way of achieving this is by using a translation library, such as Flask-Babel. 

Here are the steps to add translations to the form labels:

1. Install Flask-Babel:

```python
pip install Flask-Babel
```

2. Initialize Flask-Babel in your Flask application:

```python
from flask_babel import Babel

app = Flask(__name__)
babel = Babel(app)
```

3. Create translation files for each language you want to support. These files should contain translations for the form labels. For example, create a file named `messages.po` and add translations for the form labels:

```
msgid "Name"
msgstr "Nom"
msgid "Email"
msgstr "Email"
msgid "Submit"
msgstr "Soumettre"
```

4. Configure Flask-Babel to use the translations:

```python
app.config['BABEL_TRANSLATION_DIRECTORIES'] = 'translations'
babel.init_app(app)
```

## Handling Form Validation Messages
When it comes to form validation, WTForms provides built-in error messages. To make these messages multi-language, we can again leverage Flask-Babel.

Here's an example of how to translate form validation messages:

```python
from wtforms import ValidationError

class MyForm(Form):
    name = StringField('Name')

    def validate_name(form, field):
        if len(field.data) > 50:
            raise ValidationError(_("Name must be less than 50 characters"))
```

With the above code, the error message for the name field will be dynamically translated based on the user's language preference.

## Switching Between Languages
Finally, we may want to allow users to switch between different languages. We can achieve this by incorporating language selection into our application. Flask-Babel provides a convenient way to do this.

Here's an example of adding language selection to our application:

```python
from flask_babel import gettext

@app.route('/set-language/<language>')
def set_language(language):
    response = make_response(redirect(url_for('index')))
    response.set_cookie('language', language)
    return response
```

We can now include language selection links in our forms or templates to allow users to switch languages easily.

## Conclusion
In this article, we explored how to create multi-language forms with WTForms. By leveraging a translation library like Flask-Babel, we can easily translate form labels and validation messages, providing a seamless multi-language experience for our users.