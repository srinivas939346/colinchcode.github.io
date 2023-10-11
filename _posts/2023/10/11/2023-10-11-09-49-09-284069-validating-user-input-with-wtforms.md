---
layout: post
title: "[python] Validating user input with WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

When building web applications, it's crucial to ensure that the user input is validated and meets certain criteria before it is processed. This helps in maintaining data integrity and security. In Python, one popular library for validating user input is WTForms.

## What is WTForms?

WTForms is a library in Python that allows for easy validation and generation of complex forms. It provides a simple and flexible way to validate user input and render forms in HTML.

## Installation

To get started with WTForms, you first need to install it. Open your terminal or command prompt and run the following command:

```shell
pip install WTForms
```

## Setting up a basic form

WTForms follow an object-oriented approach to define forms. Let's start by setting up a basic form with a few input fields. Create a new file called `forms.py` and add the following code:

```python
from wtforms import Form, StringField, PasswordField, SubmitField
from wtforms.validators import DataRequired, Length

class LoginForm(Form):
    username = StringField('Username', validators=[DataRequired(), Length(min=4, max=20)])
    password = PasswordField('Password', validators=[DataRequired(), Length(min=6, max=20)])
    submit = SubmitField('Login')
```

In the code above, we import the necessary modules from WTForms and define a `LoginForm` class that extends the base `Form` class. The `username` field is defined as a `StringField` and the `password` field is defined as a `PasswordField`. We also add validators to enforce that both fields are required and have a specific length.

## Rendering the form

Now that we have defined our form, let's render it on a webpage. Create a new file called `app.py` and add the following code:

```python
from flask import Flask, render_template, request, redirect
from forms import LoginForm

app = Flask(__name__)
app.config['SECRET_KEY'] = 'your_secret_key'

@app.route('/login', methods=['GET', 'POST'])
def login():
    form = LoginForm()
    if request.method == 'POST' and form.validate():
        # Process the form data here
        return redirect('/dashboard')
    return render_template('login.html', form=form)

if __name__ == '__main__':
    app.run()
```

In the code above, we import the necessary modules, create a Flask application, and define a route `/login` for handling login requests. Inside the `login` function, we create an instance of the `LoginForm` class and check if the request method is `POST` and if the form data is valid. If it is, we can process the form data (e.g., authenticate the user). Otherwise, we render the login template along with the form.

## Creating the HTML template

To render the form, we need to create an HTML template. Create a new file called `login.html` and add the following code:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Login</title>
</head>
<body>
    <h1>Login</h1>
    <form method="POST" action="{{ url_for('login') }}">
        {{ form.hidden_tag() }}
        <div>
            {{ form.username.label() }}
            {{ form.username(size=30) }}
        </div>
        <div>
            {{ form.password.label() }}
            {{ form.password() }}
        </div>
        <div>
            {{ form.submit() }}
        </div>
    </form>
</body>
</html>
```

In the code above, we create a basic HTML form with username and password input fields. We use Jinja2 templating to render the form elements and set the form's `method` and `action` attributes.

## Running the application

To run the application, save all the files in the same directory and execute the following command in your terminal or command prompt:

```shell
python app.py
```

Visit `http://localhost:5000/login` in your web browser, and you should see the login form rendered. Try submitting the form with valid and invalid input to see the validation in action!

## Conclusion

WTForms is a powerful library in Python for validating user input and rendering complex forms. It provides a simple and flexible approach to form validation, helping you build secure and robust web applications.