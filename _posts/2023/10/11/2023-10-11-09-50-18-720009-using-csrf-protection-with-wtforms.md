---
layout: post
title: "[python] Using CSRF protection with WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

When building web applications, **Cross-Site Request Forgery (CSRF)** attacks are a common security concern. CSRF protection helps prevent malicious actors from tricking users into performing unintended actions without their consent. In this blog post, we'll look at how to integrate CSRF protection with **WTForms**, a popular form validation and rendering library for Python web applications.

## What is WTForms?

WTForms is a flexible library for form validation and rendering in Python web applications. It provides an easy-to-use interface to define forms and handle form data. WTForms helps ensure that incoming form data is valid and provides tools for rendering forms in HTML templates.

## Enabling CSRF Protection in WTForms

WTForms includes built-in support for CSRF protection. By default, it uses the `Flask-WTF` extension to handle CSRF tokens. To enable CSRF protection with WTForms, follow these steps:

1. Install the required packages:
```bash
pip install WTForms Flask-WTF
```

2. Import the necessary modules in your code:
```python
from flask_wtf.csrf import CSRFProtect
from wtforms import Form, StringField
from wtforms.validators import InputRequired
```

3. Initialize CSRF protection in your Flask application:
```python
app = Flask(__name__)
csrf = CSRFProtect(app)
```

4. Define your form by subclassing `wtforms.Form` and adding CSRF protection:
```python
class MyForm(Form):
    secret_message = StringField('Secret Message', validators=[InputRequired()])
```

5. In your Flask view function, create an instance of your form, validate it, and process the form data:
```python
@app.route('/submit', methods=['POST'])
def submit():
    form = MyForm()
    if form.validate_on_submit():
        # Process the form data
        secret_message = form.secret_message.data
        # ... more processing logic goes here ...
        return 'Form submitted successfully'
    return 'Invalid form data'
```

With these steps, you have enabled CSRF protection for your WTForms-based forms in your Flask application.

## Understanding CSRF Protection in WTForms

WTForms uses Flask's built-in CSRF protection mechanism, which adds a CSRF token to each form rendered with the `form` template helper. This token is then validated upon form submission, ensuring that the request is valid and not a CSRF attack.

The `WTForms` library takes care of adding the CSRF token field to the form automatically when the form is rendered. The CSRF token is stored in a secure session cookie and checked during form submission. If the token is missing or invalid, the form submission is rejected.

## Conclusion

By integrating CSRF protection with WTForms, we can enhance the security of our web applications and defend against CSRF attacks. WTForms, coupled with the Flask-WTF extension for CSRF token handling, provides an easy and effective way to protect our forms and ensure the integrity of user data.