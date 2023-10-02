---
layout: post
title: "[python] Follow redirects with Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

When working with web APIs or scraping web pages, you may encounter situations where the server sends a redirect response. In such cases, you need to be able to handle the redirects and retrieve the final response. The Python Requests library provides a simple way to follow redirects automatically.

In this tutorial, we will walk through how to use the `allow_redirects` parameter in the `requests.get()` method to enable auto-following of redirects.

## Table of Contents

- [Redirects and HTTP Status Codes](#redirects-and-http-status-codes)
- [Redirect Handling in Requests](#redirect-handling-in-requests)
- [Auto-following Redirects](#auto-following-redirects)
- [Conclusion](#conclusion)

## Redirects and HTTP Status Codes

When you visit a webpage, the server may respond with an HTTP **redirect response**. This is a way for the server to instruct the client (usually your web browser or API client) to retrieve the content from a different URL. Redirects are indicated by HTTP status codes in the response header, such as 301 (Moved Permanently) or 302 (Found).

Redirects can be useful for various purposes, such as load balancing, caching, or handling changes in URL structure. However, when making HTTP requests in Python, you need to handle redirects appropriately to obtain the final response from the server.

## Redirect Handling in Requests

By default, the Requests library in Python does not follow redirects automatically. If you make a request to a URL that returns a redirect response, Requests will simply return the response object representing the redirect response. This behavior is useful if you want to inspect the redirect URL or handle the redirect manually.

However, in most cases, you'll want to automatically follow redirects and retrieve the final response. To achieve this, you can use the `allow_redirects` parameter in the `requests.get()` method.

## Auto-following Redirects

To enable auto-following of redirects, simply set the `allow_redirects` parameter to `True` when making a GET request with the Requests library.

Here's an example:

```python
import requests

response = requests.get('http://example.com', allow_redirects=True)

print(response.status_code)  # Print the final response status code
print(response.url)  # Print the final URL that the request was redirected to
print(response.content)  # Print the response content
```

In the above example, we make a GET request to `http://example.com`. If the server responds with a redirect response, Requests will automatically follow the redirect and return the final response. We can then access various properties of the response object, such as `status_code`, `url`, and `content`.

By default, `allow_redirects` is set to `True`, so you don't need to explicitly specify it if you want to enable auto-following of redirects.

## Conclusion

Handling redirects is a common requirement when working with web APIs or scraping web pages. The Python Requests library provides a straightforward way to automatically follow redirects.

In this tutorial, we explored how to enable auto-following of redirects using the `allow_redirects` parameter in the `requests.get()` method. By setting `allow_redirects=True`, Requests will automatically handle the redirects and return the final response.

Now you can confidently handle redirects in your Python projects! Happy redirect handling!