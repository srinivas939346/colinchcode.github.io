---
layout: post
title: "[python] Styling forms with CSS in WTForms"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

When it comes to web development and form handling, WTForms is a powerful library in Python that makes managing forms easier. While WTForms provides the functionality to create and validate forms, it doesn't handle the styling of these forms. That's where Cascading Style Sheets (CSS) come into play.

In this blog post, we'll explore how to style forms created with WTForms using CSS.

## Table of Contents
- [Introduction to WTForms](#introduction-to-wtforms)
- [Adding External CSS File](#adding-external-css-file)
- [Styling Form Fields](#styling-form-fields)
  - [Input Fields](#input-fields)
  - [Buttons](#buttons)
  - [Labels](#labels)
- [Conclusion](#conclusion)

## Introduction to WTForms

WTForms is a flexible forms validation and rendering library in Python that makes it easy to handle forms in web applications. It provides a high-level API for creating, rendering, and validating HTML forms.

To get started with WTForms, you need to have it installed in your Python environment. You can install it using pip:

```python
pip install WTForms
```

To create a form using WTForms, you'll typically define a form class that inherits from the `wtforms.Form` class and define form fields as class attributes. For example:

```python
from wtforms import Form, StringField, SubmitField

class MyForm(Form):
    name = StringField('Name')
    email = StringField('Email')
    submit = SubmitField('Submit')
```

Once you've defined your form, you can render it in your template and handle form submission in your application.

## Adding External CSS File

To style WTForms, you can leverage CSS to customize the appearance of the form fields. First, you need to create an external CSS file, for example, `style.css`, and include it in your HTML template:

```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" type="text/css" href="style.css">
</head>
<body>
    <!-- Form code goes here -->
</body>
</html>
```

Make sure to place the `style.css` file in the same directory as your HTML template.

## Styling Form Fields

### Input Fields

To style the input fields of your form, you can target the `input` element in your CSS file. For example, to change the font color, font size, and background color of the input fields, you can use:

```css
input {
    color: #333;
    font-size: 16px;
    background-color: #f2f2f2;
}
```

You can also style specific input fields based on their `id` or `class` attributes. For example:

```css
#nameInput {
    /* CSS rules for name input field */
}

.emailInput {
    /* CSS rules for email input field */
}
```

### Buttons

To style buttons in your form, you can target the `button` or `input[type="submit"]` elements in your CSS file. For example:

```css
button {
    background-color: #007bff;
    color: #fff;
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
}

input[type="submit"] {
    /* CSS rules for submit button */
}
```

### Labels

To style labels of form fields, you can target the `label` element in your CSS file. For example:

```css
label {
    font-weight: bold;
}

.required-label {
    color: red;
}
```

## Conclusion

Using WTForms, you can easily handle forms in your Python applications. To style these forms, you can use CSS to customize the appearance of form fields, buttons, and labels. By leveraging CSS, you can create visually appealing forms that match the design of your web application.

Remember to link your external CSS file in your HTML template to apply the styles.

By combining the power of WTForms with CSS styling, you can create functional and visually appealing forms for your web applications.