---
layout: post
title: "[python] Handling form submissions with AJAX and WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

When it comes to handling form submissions in web development, Ajax is a powerful technique that allows you to send form data to the server and update parts of the webpage without reloading the entire page. In this blog post, we will explore how to handle form submissions using Ajax and WTForms, a popular form library in Python.

## Table of Contents
- [What is Ajax?](#what-is-ajax)
- [What is WTForms?](#what-is-wtforms)
- [Combining Ajax and WTForms](#combining-ajax-and-wtforms)
- [Example: Creating an AJAX form submission](#example-creating-an-ajax-form-submission)
- [Conclusion](#conclusion)

## What is Ajax?
Ajax, short for Asynchronous JavaScript and XML, is a set of web development techniques that allows you to send and receive data from the server asynchronously without interfering with the user's interaction on the webpage. With Ajax, you can update parts of the webpage dynamically, without having to reload the entire page.

## What is WTForms?
WTForms is a flexible and powerful form library in Python that helps you define and validate forms easily. It provides a simple way to handle form data, validate user input, and render HTML forms. With WTForms, you can define your forms as classes and use various field types, validators, and widgets to customize the form behavior and presentation.

## Combining Ajax and WTForms
To handle form submissions with Ajax and WTForms, you need to write JavaScript code on the client-side to capture the form data, send it to the server using Ajax, and handle the server's response. On the server-side, you can use WTForms to validate and process the form data.

## Example: Creating an AJAX form submission
Let's consider an example of a simple contact form that collects the user's name and email address. We will use Ajax and WTForms to handle the form submission asynchronously.

First, let's define the HTML form in our template:

```html
<form id="contact-form" method="POST">
  <input type="text" name="name" placeholder="Name">
  <input type="email" name="email" placeholder="Email">
  <button type="submit">Submit</button>
</form>
```

Next, we need to write JavaScript code to handle the form submission using Ajax. Here's an example using jQuery library:

```javascript
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script>
  $(document).ready(function() {
    $("#contact-form").submit(function(event) {
      event.preventDefault();  // Prevents the default form submission

      var formData = $(this).serialize();  // Serialize form data

      $.ajax({
        url: "/submit",
        type: "POST",
        data: formData,
        success: function(response) {
          alert("Form submitted successfully!");
          // Further actions or UI updates
        },
        error: function(xhr) {
          alert("Form submission failed.");
        }
      });
    });
  });
</script>
```

On the server-side, you can use WTForms to handle the form validation and processing. Here's an example using Flask as the web framework:

```python
from flask import Flask, render_template, request
from flask_wtf import FlaskForm
from wtforms import StringField, SubmitField
from wtforms.validators import DataRequired, Email

app = Flask(__name__)
app.config["SECRET_KEY"] = "your-secret-key"

class ContactForm(FlaskForm):
    name = StringField("Name", validators=[DataRequired()])
    email = StringField("Email", validators=[DataRequired(), Email()])
    submit = SubmitField("Submit")

@app.route("/", methods=["GET", "POST"])
def contact():
    form = ContactForm()

    if form.validate_on_submit():
        # Process the form data
        name = form.name.data
        email = form.email.data

        # Perform further actions or save the data

        return "success"  # Return a success response

    return render_template("contact.html", form=form)

if __name__ == "__main__":
    app.run()
```

In this example, we define a Flask route that handles both GET and POST requests. The form submission will trigger the `contact()` function, where we create an instance of `ContactForm` and validate it using `form.validate_on_submit()`. If the form is valid, we can process the form data and return a success response.

## Conclusion
Using Ajax and WTForms together allows you to enhance the user experience by handling form submissions asynchronously and validating the form data on the server. By combining the power of both tools, you can create responsive and interactive web forms. So, give it a try and start building more dynamic forms in your web applications!