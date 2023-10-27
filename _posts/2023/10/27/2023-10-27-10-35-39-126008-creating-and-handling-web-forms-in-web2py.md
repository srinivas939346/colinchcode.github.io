---
layout: post
title: "[python] Creating and handling web forms in Web2py"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

When developing web applications, handling user input through web forms is a common requirement. Web2py, a Python-based web framework, provides a simple and efficient way to handle web forms. In this blog post, we'll explore how to create and handle web forms in Web2py.

## Table of Contents
1. [Creating a Form](#creating-a-form)
2. [Handling Form Submission](#handling-form-submission)
3. [Validating Form Data](#validating-form-data)
4. [Displaying Form Errors](#displaying-form-errors)
5. [Conclusion](#conclusion)

## 1. Creating a Form<a name="creating-a-form"></a>

To create a form in Web2py, you can make use of the `SQLFORM` function. This function generates a form based on a database table or a custom form definition.

Here's a simple example of creating a form using the `SQLFORM` function:

```python
def my_form():
    form = SQLFORM(db.my_table)
    return dict(form=form)
```

In the above code, `db.my_table` represents a database table. The `SQLFORM` function generates a form based on the fields of the `my_table` table. The generated form is stored in the `form` variable, which can be passed to the view.

## 2. Handling Form Submission<a name="handling-form-submission"></a>

Once the form is created, you need to handle the form submission to process the user input. Web2py provides a convenient way to handle form submission using the `form.accepts()` function.

Here's an example of handling form submission in Web2py:

```python
def my_form():
    form = SQLFORM(db.my_table)
    
    if form.accepts(request.vars, session):
        # Process form data and perform necessary actions
        redirect(URL('success'))
        
    return dict(form=form)
```

In the above code, `form.accepts()` checks if the submitted form data is valid. If the data is valid, the code inside the `if` block is executed. You can perform any necessary actions like saving the form data to the database or sending an email. Finally, you can use `redirect()` to redirect the user to a success page or any other page.

## 3. Validating Form Data<a name="validating-form-data"></a>

Validating form data is crucial to ensure the accuracy and integrity of the submitted data. Web2py provides built-in form validators to validate form data.

Here's an example of applying validators to form fields in Web2py:

```python
def my_form():
    form = SQLFORM(db.my_table)
    
    # Apply validators to form fields
    form.custom.widget.my_field.requires = IS_NOT_EMPTY()
    
    if form.accepts(request.vars, session):
        redirect(URL('success'))
        
    return dict(form=form)
```

In the above code, `IS_NOT_EMPTY()` is a built-in validator that ensures the `my_field` form field is not empty. You can apply various validators to different form fields, depending on your requirements.

## 4. Displaying Form Errors<a name="displaying-form-errors"></a>

When a form submission fails due to validation errors, it's essential to display those errors to the user. Web2py makes it easy to display form errors using the `form.errors` attribute.

Here's an example of displaying form errors in Web2py:

```python
def my_form():
    form = SQLFORM(db.my_table)
    
    if form.accepts(request.vars, session):
        redirect(URL('success'))
        
    return dict(form=form)
```

In the above code, after the `if form.accepts()` block, you can add the following code in the view to display form errors:

```python
{{if form.errors:}}
    <div class="alert alert-danger">
        Please correct the following errors:
        <ul>
            {{for field, error in form.errors.items():}}
                <li>{{=error}}</li>
            {{pass}}
        </ul>
    </div>
{{pass}}
```

The above code loops through the `form.errors` dictionary and displays each error message. You can customize the error message display as per your application's styling requirements.

## 5. Conclusion<a name="conclusion"></a>

Handling web forms is an integral part of web application development, and Web2py provides a straightforward approach to achieve this. In this blog post, we discussed how to create forms using the `SQLFORM` function, handle form submission, validate form data, and display form errors in Web2py. Make use of these techniques to create robust and user-friendly web forms in your Web2py applications.

For more information and detailed documentation, refer to the official [Web2py documentation](https://www.web2py.com).