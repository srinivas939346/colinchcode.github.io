---
layout: post
title: "[python] Handling form data in CherryPy using WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---
In web development, it is common to encounter situations where you need to handle form data. CherryPy, a minimalist Python web framework, provides a simple and efficient way to handle form data using WTForms.

## What is WTForms?
WTForms is a flexible forms validation and rendering library for Python. It allows you to define forms as classes, validate user input, and render form fields.

## Installing WTForms
To use WTForms in your CherryPy project, you need to install it first. You can install WTForms using pip by running the following command:

```bash
pip install WTForms
```

## Creating a form class
To handle form data with WTForms, you need to define a form class that subclasses `wtforms.Form`. Inside the form class, you can define form fields using different field types provided by WTForms.

Here's an example of a simple form class that contains two fields: a `StringField` for the username and a `PasswordField` for the password:

```python
import wtforms

class LoginForm(wtforms.Form):
    username = wtforms.StringField('Username')
    password = wtforms.PasswordField('Password')
```

In the above example, we import `wtforms` and define a `LoginForm` class that subclasses `wtforms.Form`. We define two fields, `username` and `password`, as instances of `wtforms.StringField` and `wtforms.PasswordField`, respectively. The field label is passed as a parameter to each field.

## Rendering the form in a CherryPy view
Now that we have defined a form class, we can render the form in a CherryPy view. In the view function, we initialize the form class and pass it to the template for rendering.

```python
import cherrypy
from jinja2 import Environment, FileSystemLoader
from wtforms import (StringField, PasswordField)
from wtforms.validators import (DataRequired, Length)

env = Environment(loader=FileSystemLoader('<path_to_templates_folder>'))

class MyApplication:
    @cherrypy.expose
    def login(self):
        form = LoginForm()
        tmpl = env.get_template('login.html')
        return tmpl.render(form=form)

if __name__ == '__main__':
    cherrypy.quickstart(MyApplication())
```

In the above example, we import the necessary modules and set up the Jinja2 template environment. We define a `login` method in the `MyApplication` class, which is exposed as a CherryPy URL. Inside the method, we initialize an instance of the `LoginForm` class and pass it to the `login.html` template for rendering.

## Handling form submission
To handle form submission and validate user input, we can modify the `login` method in the CherryPy view.

```python
    @cherrypy.expose
    def login(self, username=None, password=None):
        form = LoginForm()
        if cherrypy.request.method == 'POST':
            form = LoginForm(cherrypy.request.params)
            if form.validate():
                # Process the form data
                # Redirect or return a success message
                pass
        tmpl = env.get_template('login.html')
        return tmpl.render(form=form)
```

In the modified `login` method, we check if the request method is `POST`. If it is, we initialize the `LoginForm` class with the request parameters and validate the form. If the form is valid, we can process the form data, such as authenticating the user or saving the data to a database.

## Conclusion
WTForms provides a convenient way to handle form data in CherryPy by defining form classes and rendering them in views. By utilizing WTForms' validation and rendering features, you can easily handle and validate user input in your CherryPy applications.