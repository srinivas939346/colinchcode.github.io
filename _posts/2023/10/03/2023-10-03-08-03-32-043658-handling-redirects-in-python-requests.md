---
layout: post
title: "[python] Handling redirects in Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

When making HTTP requests using the `requests` library in Python, it's common to come across redirects. A redirect is when the server responds with a status code `3xx` and a `Location` header, which indicates the new URL that the client should redirect to.

In this tutorial, we'll learn how to handle redirects when using `requests` library in Python.

## Table of Contents

1. [Redirects and their codes](#redirects-and-their-codes)
2. [Automatically following redirects](#automatically-following-redirects)
3. [Customizing redirect behavior](#customizing-redirect-behavior)
4. [Handling redirect loops](#handling-redirect-loops)
5. [Conclusion](#conclusion)

## Redirects and their codes

In HTTP, redirects are indicated by status codes in the `3xx` range. Here are some common redirect status codes:

- `301 Moved Permanently` - The requested resource has been permanently moved to a new URL.
- `302 Found` - The requested resource has been temporarily moved to a different URL.
- `303 See Other` - The response to the request can be found at a different URL.
- `307 Temporary Redirect` - The requested resource is temporarily available at a different URL.

These are just a few examples, and there are more status codes that indicate different types of redirects.

## Automatically following redirects

By default, `requests` library automatically handles redirects for you. When making a request, if a redirect status code is received, `requests` will automatically follow the redirect and return the response.

Here's an example:

```python
import requests

response = requests.get('https://example.com')
print(response.url)  # Prints the final URL after following redirects
```

The `requests.get()` method automatically follows any redirects and returns the response for the final redirected URL. You can then access the redirected URL using the `url` attribute of the response object.

## Customizing redirect behavior

If you want to customize the behavior of redirects, you can use the `allow_redirects` parameter of the `requests` methods. By default, `allow_redirects` is set to `True`.

Here's an example where we disable automatic redirects:

```python
import requests

response = requests.get('https://example.com', allow_redirects=False)
print(response.status_code)  # Prints the redirect status code
```

In this case, the `requests.get()` method will not automatically follow the redirect and simply return the response with the redirect status code.

## Handling redirect loops

Sometimes, you might encounter redirect loops where the same URL is being redirected to itself in a loop. To prevent infinite redirects, `requests` library has a built-in mechanism that limits the number of redirects to follow.

By default, the maximum number of redirects allowed is 30. If the limit is reached, `requests` will raise a `TooManyRedirects` exception.

Here's an example:

```python
import requests

try:
    response = requests.get('https://example.com/redirect-loop')
except requests.TooManyRedirects:
    print("Too many redirects")
```

In this example, if the URL `https://example.com/redirect-loop` results in a redirect loop, `requests` will raise a `TooManyRedirects` exception.

To handle redirect loops, you can either increase the maximum number of redirects by setting the `max_redirects` parameter, or catch the `TooManyRedirects` exception and handle it accordingly.

## Conclusion

Handling redirects in Python Requests is straightforward. By default, `requests` automatically handles redirects for you, but you can customize this behavior by using the `allow_redirects` parameter. Additionally, there are built-in mechanisms to handle redirect loops and limit the number of redirects.

Being able to handle redirects efficiently is important when building web scrapers, working with APIs, or interacting with HTTP-based services. By understanding how redirects work and using the `requests` library, you can handle them seamlessly in your Python applications.