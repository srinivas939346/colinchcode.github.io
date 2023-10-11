---
layout: post
title: "[python] Handling file uploads with WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

When working with web applications, it's common to require the ability to upload files from users. In Python, WTForms is a popular tool for handling form validation and data handling. In this blog post, we'll explore how to handle file uploads using WTForms.

### Prerequisites

Before we get started, make sure you have the following dependencies installed:

- Python (version 3 or above)
- Flask
- WTForms

You can install Flask and WTForms using pip:

```shell
pip install flask wtforms
```

### HTML form

To create a file upload form, we'll start by creating an HTML form. In your HTML template file, create a form with the `enctype` attribute set to `"multipart/form-data"`. This tells the browser that the form will contain file data.

```html
<form action="/upload" method="post" enctype="multipart/form-data">
  <input type="file" name="file">
  <button type="submit">Upload</button>
</form>
```

### Flask route

In your Flask application, create a route to handle the file upload. We'll use the `FileField` class from WTForms to represent the file input field.

```python
from flask import Flask, render_template, request
from flask_wtf import FlaskForm
from wtforms import FileField

app = Flask(__name__)
app.secret_key = "my-secret-key"

class MyForm(FlaskForm):
    file = FileField('Upload file')

@app.route('/', methods=['GET', 'POST'])
def upload_file():
    form = MyForm()
    if form.validate_on_submit():
        file = form.file.data
        # Handle the uploaded file here
        return "File uploaded successfully"
    return render_template('upload.html', form=form)
```

### Handling the file

When the form is submitted, the `form.validate_on_submit()` method triggers the form validation and checks if the file field is valid. We can retrieve the uploaded file using `form.file.data`. From there, you can perform any necessary processing or saving of the file.

Remember to handle any exceptions that may occur while working with the uploaded file, such as file size limit exceeded or invalid file format.

### Conclusion

In this blog post, we covered how to handle file uploads with WTForms in Python. By using the `FileField` class and following the proper HTML form setup, you can easily handle file uploads in your web applications. Remember to always validate and handle the uploaded file properly to ensure security and smooth user experience.