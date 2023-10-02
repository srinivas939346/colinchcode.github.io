---
layout: post
title: "[python] Handling response status codes in Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

When making HTTP requests with Python, the `requests` library is a commonly used choice. One important aspect of working with requests is handling the response status codes returned by the server.

Status codes indicate the outcome of an HTTP request. They provide useful information about whether a request was successful, encountered an error, or required further action. In `requests`, status codes are represented by the `Response` object's `status_code` attribute.

Here, we will cover how to handle different response status codes using `requests` in Python.

## Checking for a Successful Request

A status code starting with `2` indicates a successful request. The most common success status code is `200`, which signifies a successful HTTP GET request. To check if a request was successful, you can compare the `status_code` with the `requests.codes.ok` constant, which represents a status code of `200`.

```python
import requests

response = requests.get("https://example.com")

if response.status_code == requests.codes.ok:
    # Request succeeded, do something
    print("Request was successful")
else:
    # Request failed, handle the error
    print("Request failed with status code:", response.status_code)
```

In the example above, we make a `GET` request to `https://example.com` and check if the response status code is equal to `200`. If the request was successful, we perform the desired actions. Otherwise, we handle the error by printing the status code.

## Handling Common Status Codes

Some commonly encountered status codes include:

- `404` - Page not found: This code indicates that the requested resource was not found on the server.
- `401` - Unauthorized: Indicates that the request requires authentication, and the client did not provide valid credentials.
- `500` - Internal Server Error: This code indicates a server-side error occurred while processing the request.

To handle these status codes, you can simply compare the `status_code` with the desired status code and take appropriate action.

```python
if response.status_code == 404:
    print("Page not found")
elif response.status_code == 401:
    print("Unauthorized request")
elif response.status_code == 500:
    print("Internal server error")
else:
    print("Unknown status code:", response.status_code)
```

## Handling Redirects

HTTP requests sometimes return status codes indicating that the requested resource has moved to a different location. Example status codes for redirects are `301` (Moved Permanently) and `302` (Found).

By default, `requests` automatically follows redirects for `GET` requests. However, if you need to handle redirects manually, you can set the `allow_redirects` parameter to `False` in your request. The response will then have the `status_code` set to `301` or `302`, depending on the redirect encountered.

```python
response = requests.get("https://example.com", allow_redirects=False)

if response.status_code == 301 or response.status_code == 302:
    print("Redirect encountered")
    print("Redirect location:", response.headers["Location"])
else:
    print("No redirect occurred")
```

In the example above, we disable redirect following and check if a redirect occurred by comparing the `status_code` with `301` or `302`. If a redirect occurred, we can access the redirect location from the `Location` header.

## Conclusion

Handling response status codes is an essential part of working with HTTP requests in Python. By checking and handling different status codes appropriately, you can ensure your code responds correctly to various scenarios encountered while making requests using the `requests` library.