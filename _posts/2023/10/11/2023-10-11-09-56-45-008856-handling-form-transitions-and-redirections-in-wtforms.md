---
layout: post
title: "[python] Handling form transitions and redirections in WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

When working with web forms in Python, WTForms is a popular choice due to its simplicity and flexibility. It provides an easy way to create and validate forms in web applications.

One common requirement in web forms is to handle form transitions and redirections. For example, after submitting a form, you may want to redirect the user to a different page or show a success message. In this blog post, we'll explore how to handle these transitions and redirections using WTForms.

## Using Flask-WTF with WTForms

Before we dive into handling transitions and redirections, let's first set up a basic Flask application with Flask-WTF and WTForms. Make sure you have [Flask](https://flask.palletsprojects.com/) and [Flask-WTF](https://flask-wtf.readthedocs.io/) installed on your system.

```python
from flask import Flask, render_template, redirect, url_for
from flask_wtf import FlaskForm
from wtforms import StringField, SubmitField
from wtforms.validators import DataRequired

app = Flask(__name__)
app.config['SECRET_KEY'] = 'your-secret-key'

class MyForm(FlaskForm):
    name = StringField('Name', validators=[DataRequired()])
    submit = SubmitField('Submit')

@app.route('/', methods=['GET', 'POST'])
def index():
    form = MyForm()

    if form.validate_on_submit():
        # Handle form submission

        return redirect(url_for('success'))

    return render_template('index.html', form=form)

@app.route('/success')
def success():
    return render_template('success.html')

if __name__ == '__main__':
    app.run()
```

In this code snippet, we define a basic Flask application with a simple form. The form has a single input field, `name`, and a submit button. When the form is submitted, it validates the input and if everything is correct, it redirects the user to the `success` endpoint.

## Redirection after form submission

To redirect the user to a different page after form submission, we use the `redirect` function from Flask. This function takes a URL as a parameter and redirects the user to that URL.

In our example code, after the form is validated and submitted, we use `redirect(url_for('success'))` to redirect the user to the `success` endpoint. The `url_for` function generates the URL for the given endpoint. In this case, it generates the URL for the `success` endpoint.

## Displaying success message

After successfully submitting the form, you may want to display a success message to the user. To achieve this, you can create a separate HTML template for the success page and render it when the user is redirected to that page.

Create a `success.html` template with the following content:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Form Success</title>
</head>
<body>
    <h1>Form Submitted Successfully!</h1>
    <p>Thank you for submitting the form.</p>
</body>
</html>
```

In the `success` endpoint, we render this template using `render_template('success.html')`, which will display the success message to the user.

## Conclusion

Handling form transitions and redirections is a common requirement when working with web forms. In this blog post, we explored how to handle these transitions and redirections using WTForms in a Flask application. We learned how to redirect the user after form submission and display a success message. This will help you build more user-friendly web forms using WTForms.

Remember to always validate the form data on the server-side to ensure data integrity and security.