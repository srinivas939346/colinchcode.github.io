---
layout: post
title: "[python] Working with controllers in Web2py"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Web2py is a popular Python web framework that follows the MVC (Model-View-Controller) architectural pattern. In this blog post, we will explore how to work with controllers in Web2py.

## Table of Contents
- [Introduction to Controllers](#introduction-to-controllers)
- [Creating a Controller](#creating-a-controller)
- [Defining Actions](#defining-actions)
- [Parameters and HTTP Methods](#parameters-and-http-methods)
- [Redirecting and Rendering Views](#redirecting-and-rendering-views)
- [Conclusion](#conclusion)

## Introduction to Controllers

In Web2py, a controller is a Python module that handles HTTP requests and determines the actions to be executed based on the URLs. It acts as an intermediary between the incoming requests and the models and views.

## Creating a Controller

To create a controller in Web2py, you need to create a Python module with a `.py` extension in the `controllers` directory. Let's assume we are working on a blog application and want to create a controller to handle blog posts. We can create a file named `post.py` in the `controllers` directory.

```python
# controllers/post.py

def index():
    # Code for handling the /post/index URL
    return dict()

def create():
    # Code for handling the /post/create URL
    return dict()

def edit():
    # Code for handling the /post/edit URL
    return dict()
```

In the above code, we defined three actions: `index`, `create`, and `edit`. Each action is a Python function that handles a specific URL.

## Defining Actions

Actions in Web2py are defined as Python functions within the controller module. Each action represents a specific URL or route. In the code example above, the `index` action handles the `/post/index` URL, the `create` action handles the `/post/create` URL, and the `edit` action handles the `/post/edit` URL.

Inside each action, you can write code to perform various tasks such as fetching data from the database, validating user input, and rendering views.

## Parameters and HTTP Methods

URL parameters can be passed to actions in Web2py. For example, if you have an action that handles the URL `/post/show/123`, the `123` part can be accessed as a parameter in the action function.

To handle different HTTP methods (GET, POST, PUT, DELETE, etc.), you can define separate functions within an action. For example, to handle a post request for creating a new blog post, you can define a function named `create_POST()`.

## Redirecting and Rendering Views

Controllers in Web2py can redirect to other actions or URLs using the `redirect()` function. For example, after successfully creating a blog post, you can redirect the user to the post's detail page.

To render views, you can use the `response.view` attribute. By default, Web2py will associate views with the same name as the actions. You can customize the view name or template by setting `response.view` to the desired value.

```python
def index():
    posts = db(db.post).select()
    return dict(posts=posts)

def create():
    form = SQLFORM(db.post)
    if form.process().accepted:
        redirect(URL('post', 'index'))
    return dict(form=form)
```

In the above example, the `index` action fetches all posts from the database and passes them to the corresponding view. The `create` action displays a form to create a new post. If the form submission is successful, the user is redirected to the `index` action.

## Conclusion

Controllers are an essential part of Web2py, as they handle HTTP requests and determine the actions to be executed. In this blog post, we explored how to create controllers, define actions, handle parameters and HTTP methods, and redirect and render views. Understanding controllers is crucial for building dynamic and interactive web applications using Web2py.