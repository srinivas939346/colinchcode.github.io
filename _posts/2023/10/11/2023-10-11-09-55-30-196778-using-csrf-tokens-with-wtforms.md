---
layout: post
title: "[python] Using CSRF tokens with WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---
When building web applications, it is crucial to protect against cross-site request forgery (CSRF) attacks. CSRF attacks occur when an attacker tricks a victim into performing unwanted actions on a website using the victim's authenticated session.

One way to mitigate CSRF attacks is by using CSRF tokens. Here, we'll explore how to use CSRF tokens with WTForms, a popular form validation and rendering library in Python.

## What is WTForms?
WTForms is a library built on top of Flask-WTF that provides flexible, secure, and reusable form validation and rendering. It helps simplify form handling by providing a consistent interface for defining, validating, and rendering forms.

## Setup
Before using CSRF protection with WTForms, make sure you have Flask-WTF installed. You can install it using pip:

```bash
pip install Flask-WTF
```

## Enabling CSRF protection in WTForms
To enable CSRF protection in WTForms, you need to configure it in your Flask application. This can be done by setting the `SECRET_KEY` configuration option.

Open your Flask application's configuration file (e.g., `config.py`) and add the following line:

```python
SECRET_KEY = 'your_secret_key_here'
```

Make sure to use a strong and random secret key.

## Generating and Using CSRF Tokens with WTForms
WTForms automatically generates and includes CSRF tokens in the HTML form when the CSRF protection is enabled. Here's an example of a Flask route that renders a form using WTForms:

```python
from flask import Flask, render_template
from flask_wtf.csrf import CSRFProtect
from forms import MyForm

app = Flask(__name__)
app.config.from_pyfile('config.py')
CSRFProtect(app)

@app.route('/my-form', methods=['GET', 'POST'])
def my_form():
    form = MyForm()
    if form.validate_on_submit():
        # Process the form data
        return 'Form submitted successfully!'
    return render_template('my-form.html', form=form)

if __name__ == '__main__':
    app.run()
```

Here, we imported `CSRFProtect` from `flask_wtf.csrf` to enable CSRF protection. The `CSRFProtect(app)` line initializes CSRF protection for our Flask application.

In the `my_form` route, we create an instance of `MyForm` (which is a WTForm class) and pass it to the template for rendering. WTForms automatically includes the CSRF token for this form.

## Using CSRF token in HTML form
To use the CSRF token in your HTML form, you can render the form using WTForms in your template:

```html
<form method="POST" action="">
    {{ form.csrf_token }}
    {{ form.field.label }} {{ form.field() }}
    {{ form.submit() }}
</form>
```

Here, `{{ form.csrf_token }}` renders the CSRF token as a hidden field in the form. This token is automatically validated when the form is submitted.

## Conclusion
Protecting against CSRF attacks is essential for web application security. By using CSRF tokens with WTForms, you can significantly reduce the risk of CSRF attacks on your Flask web applications. Remember to always include the CSRF token in your forms to ensure protection.