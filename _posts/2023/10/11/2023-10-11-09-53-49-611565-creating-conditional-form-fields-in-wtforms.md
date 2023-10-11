---
layout: post
title: "[python] Creating conditional form fields in WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

WTForms is a widely used library in Python for building web forms. It provides an easy and flexible way to define and validate form fields. In some cases, you may want to show or hide form fields based on certain conditions. This can be easily accomplished using conditional form fields in WTForms.

In this blog post, we will explore how to create conditional form fields in WTForms with some examples.

### Setup

Before we begin, make sure you have WTForms installed in your Python environment. You can install it using pip:

```python
pip install wtforms
```

### Creating a Simple Form

Let's start by creating a simple form using WTForms. Suppose we want to create a form to gather user information, such as name, email, and age. Here's an example of how to define the form using WTForms:

```python
from wtforms import Form, StringField, IntegerField, SubmitField

class UserInfoForm(Form):
    name = StringField('Name')
    email = StringField('Email')
    age = IntegerField('Age')
    submit = SubmitField('Submit')
```

### Adding Conditional Fields

Now let's say we want to show an additional field for the user's address, but only if the user is above a certain age. We can achieve this by adding a conditional field to our form. Here's an example:

```python
from wtforms import ValidationError

class UserInfoForm(Form):
    name = StringField('Name')
    email = StringField('Email')
    age = IntegerField('Age')
    address = StringField('Address')

    def validate_age(form, field):
        if form.age.data is not None and form.age.data < 18:
            raise ValidationError('You must be 18 or older to enter an address.')
        if form.age.data is not None and form.age.data >= 18 and form.address.data == '':
            raise ValidationError('Please provide an address.')

    submit = SubmitField('Submit')
```

In the above example, we added an additional field called `address` to our form. We also defined a custom validation method `validate_age` to handle the conditions for showing or hiding the address field. If the user is below 18 years old, an error message will be displayed. If the user is 18 or older, the address field will be required. If the age is not provided, the address field will remain hidden.

### Displaying the Form

To display the form in a web application, we can use a Flask route as an example:

```python
from flask import Flask, render_template, request
from wtforms import StringField, IntegerField, SubmitField
from wtforms.validators import InputRequired
from wtforms import ValidationError

app = Flask(__name__)
app.config['SECRET_KEY'] = 'your_secret_key'

@app.route('/', methods=['GET', 'POST'])
def index():
    form = UserInfoForm(request.form)

    if request.method == 'POST':
        if form.validate():
            # Handle form submission here
            pass

    return render_template('index.html', form=form)

if __name__ == '__main__':
    app.run()
```

In the above example, we define a route for the root URL ("/") and render the form using the `render_template` function from Flask. We also handle form submission by checking if the form is valid. You can customize the handling of form submission according to your application's needs.

### Conclusion

Using conditional form fields in WTForms allows you to create dynamic and interactive forms with ease. You can show or hide form fields based on certain conditions, making the user experience smoother and more personalized. By following the examples provided in this blog post, you can easily implement conditional form fields in your next web application.