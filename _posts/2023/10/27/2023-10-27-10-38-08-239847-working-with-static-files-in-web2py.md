---
layout: post
title: "[python] Working with static files in Web2py"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Web2py is a popular Python web framework that provides a convenient way to serve static files such as images, CSS stylesheets, and JavaScript files. In this article, we will discuss how to work with static files in Web2py.

## Table of Contents

1. [Setting up the static folder](#setting-up-the-static-folder)
2. [Linking to static files](#linking-to-static-files)
3. [Handling static file requests](#handling-static-file-requests)
4. [Conclusion](#conclusion)

## Setting up the static folder

By default, Web2py looks for static files in the `applications/{your_app_name}/static` folder. If this folder doesn't exist, you can create it manually. Inside the `static` folder, you can organize your files into subdirectories as per your requirement. For example, you can have separate folders for `css`, `js`, and `images`.

Here's an example of how the directory structure might look like:

```
applications/
    your_app_name/
        static/
            css/
                styles.css
            js/
                script.js
            images/
                logo.png
```

## Linking to static files

To link to a static file in your Web2py templates or views, you can use the `URL` helper function. The `URL` function accepts two parameters: the type of the static file and the file path.

For example, to link to the `styles.css` file in the `css` subdirectory, you can use the following code:

```html
<link rel="stylesheet" type="text/css" href="{{=URL('static', 'css/styles.css')}}">
```

Similarly, to link to the `logo.png` image in the `images` subdirectory, you can use the following code:

```html
<img src="{{=URL('static', 'images/logo.png')}}">
```

## Handling static file requests

By default, Web2py handles static file requests automatically. When a static file is requested, Web2py looks for it in the `static` folder and serves it directly without involving the controllers or models. This improves performance by bypassing unnecessary processing.

However, if you need to perform some additional logic before serving a static file, you can create a controller to handle the request. To do this, you need to create a function in your controller that matches the requested file path.

For example, let's say you want to perform some authentication before serving the `styles.css` file in the `css` subdirectory. You can create a controller function like this:

```python
def styles():
    # Perform authentication logic here
    return response.stream('applications/your_app_name/static/css/styles.css')
```

Now, when you link to the `styles.css` file in your template, you would use the following code:

```html
<link rel="stylesheet" type="text/css" href="{{=URL('controller', 'styles')}}">
```

## Conclusion

Working with static files in Web2py is straightforward. By following the conventions and utilizing the `URL` helper function, you can link to static files easily. Additionally, if you need to handle static file requests differently, you can create a controller function to perform custom logic.

References:
- [Web2py official documentation](http://web2py.com/books/default/chapter/29/04/static-files-and-upload)
- [Web2py static files](http://web2py.org/examples/static_files.html)