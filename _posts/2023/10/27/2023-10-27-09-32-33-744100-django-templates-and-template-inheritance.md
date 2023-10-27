---
layout: post
title: "[python] Django templates and template inheritance"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

When developing web applications with Django, **templates** play a crucial role in separating the design and presentation layer from the backend logic. Django's template system provides an intuitive way to define HTML templates and render dynamic content.

## What are Django Templates?

In Django, a template is a file containing HTML code with placeholders for dynamic content. These placeholders, called **template variables**, are replaced with actual values during the rendering process. Django templates also support control structures, filters, and template tags to manipulate and display data.

## Creating a Simple Template

To create a basic Django template, create a file with a `.html` extension and define your HTML code. For example, let's create a template named `example.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Django Template</title>
</head>
<body>
    <h1>Welcome, {{ name }}!</h1>
    <p>This is a simple Django template.</p>
</body>
</html>
```

In this template, `{{ name }}` is a placeholder that will be replaced with an actual value when the template is rendered.

## Using Template Variables

To render a template with dynamic data, you can pass a dictionary of variables to the `render()` function in Django views. For example:

```python
# views.py
from django.shortcuts import render

def my_view(request):
    context = {'name': 'John'}
    return render(request, 'example.html', context)
```

In this example, we pass the `context` dictionary to the `render()` function along with the `example.html` template. The value of `name` in the context dictionary will replace the `{{ name }}` placeholder in the template when it is rendered.

## Template Inheritance

Django templates provide **template inheritance**, which allows you to create a base template with common elements and extend it in child templates. This helps in reusing code and maintaining a consistent layout across multiple pages.

To create a base template, define the common elements such as header, footer, and navigation in a parent template, let's say `base.html`:

```html
<!-- base.html -->
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}My Website{% endblock %}</title>
</head>
<body>
    {% block content %}
    {% endblock %}
</body>
</html>
```

In this base template, we define two **blocks**: `title` and `content`. The `title` block is used to specify the title of the page, and the `content` block is used to define the unique content of each child template.

To extend the `base.html` template, create a child template and inherit the base template using the `{% extends %}` tag:

```html
<!-- child.html -->
{% extends 'base.html' %}

{% block title %}My Child Page{% endblock %}

{% block content %}
    <h1>Welcome to my child page!</h1>
    <p>This page extends the base template.</p>
{% endblock %}
```

In this child template, we override the `title` block and provide unique content in the `content` block.

During the rendering process, Django combines the base template and child template to produce the final HTML output, where the blocks in the child template replace the corresponding blocks in the base template.

## Conclusion

Django templates and template inheritance are powerful tools for creating dynamic and reusable HTML layouts in Django web applications. By separating the design and logic, templates enable developers to build maintainable and scalable applications easily.

For more information, you can refer to the official [Django documentation on templates](https://docs.djangoproject.com/en/3.2/topics/templates/).