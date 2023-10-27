---
layout: post
title: "[python] Implementing user-friendly URLs and routing in Web2py"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Web2py is a powerful and user-friendly web framework built on top of the Python programming language. It offers a range of features to help developers build web applications quickly and efficiently. In this blog post, we will explore how to implement user-friendly URLs and routing in a Web2py application.

## Table of Contents
1. [Introduction](#introduction)
2. [Setting Up Routes](#setting-up-routes)
3. [Creating Controller Functions](#creating-controller-functions)
4. [Generating Links](#generating-links)
5. [Conclusion](#conclusion)

## Introduction
User-friendly URLs are essential for any web application as they provide a better experience for users and can improve search engine optimization (SEO). By default, Web2py uses a method called "URL rewriting" to achieve user-friendly URLs. However, this method requires modifying the .htaccess file and is not the most convenient approach.

In Web2py, you can use the `routes.py` file to define custom URL routes and map them to controller functions.

## Setting Up Routes
To get started, create a `routes.py` file in your application's root directory if it doesn't already exist. In this file, you can define your custom URL routes using regular expressions. For example, let's say we have a `default` controller with a `index` function, and we want to map the URL `/home` to this function. We can add the following route:

```python
routers = dict(
    BASE = dict(
        default_application='your_app',
        default_controller='default',
        default_function='index',
        map=[('/home', '/your_app/default/index')]
    )
)
```

By adding this route, every time a user visits `/home`, the `index` function in the `default` controller of the `your_app` application will be called.

You can add multiple routes by appending them to the `map` list.

## Creating Controller Functions
Next, let's create a controller function that will be called when a specific URL is accessed. In our example, we have already defined the `index` function in the `default` controller. Make sure the function accepts the necessary parameters if required.

```python
def index():
    return dict()
```

This function can include any logic you need, such as querying the database, processing form data, or rendering a template.

## Generating Links
Now that you have set up custom URL routes and controller functions, you can generate links dynamically in your views or controller functions using the `URL()` function provided by Web2py. The `URL()` function ensures that the generated link matches the configured routes.

```python
{{=URL('default', 'index')}}
```

In this example, the link generated will be `/your_app/default/index`. You can also pass additional parameters to the `URL()` function to generate URLs with query strings or route parameters.

## Conclusion
Implementing user-friendly URLs and routing in Web2py is straightforward and can greatly enhance the usability and SEO-friendliness of your web application. By defining custom routes in the `routes.py` file, mapping them to controller functions, and using the `URL()` function to generate links, you can create a seamless and intuitive experience for your users.

Web2py provides a range of other features and functionalities to explore, so be sure to check out the official documentation for more information.

**References:**
- [Web2py official documentation](https://www.web2py.com/books/default/chapter/29/05/overview#URL-rewriting)
- [Web2py GitHub repository](https://github.com/web2py/web2py)