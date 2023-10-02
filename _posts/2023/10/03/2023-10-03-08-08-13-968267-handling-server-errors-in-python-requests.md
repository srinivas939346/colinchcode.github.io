---
layout: post
title: "[python] Handling server errors in Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

When making HTTP requests in Python, the `requests` library is a popular choice. It provides a simple and intuitive API for sending HTTP requests and handling responses. However, it's important to handle server errors gracefully to provide a smooth experience to users and handle unexpected issues that may arise.

In this article, we'll explore how to handle server errors in Python requests and discuss best practices for error handling.

## Table of Contents
1. [Introduction](#introduction)
2. [Error response codes](#error-response-codes)
3. [Checking for errors](#checking-for-errors)
4. [Handling specific errors](#handling-specific-errors)
5. [Retrying requests](#retrying-requests)
6. [Conclusion](#conclusion)

## Introduction <a name="introduction"></a>

When making an HTTP request using `requests`, the server may respond with an error status code to indicate that something went wrong. These status codes fall into the 4xx and 5xx ranges, such as 400 Bad Request or 500 Internal Server Error.

By default, `requests` will raise an exception for any response with an error status code. However, we can handle these exceptions and perform custom actions based on the specific error.

## Error response codes <a name="error-response-codes"></a>

To handle server errors, we first need to be familiar with the most common error response codes:

- 400 Bad Request: The server cannot process the request due to a client error, such as invalid parameters or missing data.
- 401 Unauthorized: The request requires authentication, and the client does not provide valid credentials.
- 403 Forbidden: The server refuses to fulfill the request, even if valid authentication credentials are provided.
- 404 Not Found: The server cannot find the requested resource.
- 500 Internal Server Error: A general server error occurred, and the request could not be completed.

These are just a few examples of common error codes. There are many more that you may encounter while working with different APIs and services.

## Checking for errors <a name="checking-for-errors"></a>

To check for an error response, we can use the `raise_for_status()` method provided by the `Response` object returned by `requests`. This method will raise an exception if the response contains an error status code.

```python
import requests

response = requests.get('https://api.example.com/data')
response.raise_for_status()  # Raises an exception if the response has an error status code
```

If an exception is raised, we can catch it and handle the error appropriately. For example, we could log the error message, display a friendly error message to the user, or attempt to recover from the error.

```python
import requests

try:
    response = requests.get('https://api.example.com/data')
    response.raise_for_status()
except requests.exceptions.HTTPError as e:
    print(f"An error occurred: {e}")
```

By catching the `HTTPError` exception, we can retrieve the error message and perform any necessary actions.

## Handling specific errors <a name="handling-specific-errors"></a>

In addition to handling general HTTP errors, we may also want to handle specific error codes differently. For example, we may want to retry the request if we receive a 429 Too Many Requests error or handle authentication failures differently.

To handle specific errors, we can inspect the status code of the response and take action accordingly.

```python
import requests

response = requests.get('https://api.example.com/data')

if response.status_code == 429:
    # 429 Too Many Requests: Implement custom logic to handle rate limiting
    print("Too many requests. Please try again later.")
elif response.status_code == 401:
    # 401 Unauthorized: Handle authentication failure
    print("Unauthorized. Please provide valid credentials.")
else:
    # Handle other errors
    response.raise_for_status()
```

By checking the specific status codes, we can tailor our error handling based on the requirements of the API or service we are interacting with.

## Retrying requests <a name="retrying-requests"></a>

In some cases, it may be appropriate to retry a request when an error occurs. For example, if the server returns a 500 Internal Server Error, it might be a temporary issue that could be resolved with a subsequent request.

The `requests` library also provides support for automatic request retries using the `Retry` object from the `urllib3` library.

```python
import requests
from requests.adapters import HTTPAdapter
from urllib3.util.retry import Retry

session = requests.Session()

retries = Retry(total=3, backoff_factor=0.5)
adapter = HTTPAdapter(max_retries=retries)

session.mount('http://', adapter)
session.mount('https://', adapter)

try:
    response = session.get('https://api.example.com/data')
    response.raise_for_status()
except requests.exceptions.RequestException as e:
    print(f"An error occurred: {e}")
```

In the example above, we create a `Session` object and mount the `HTTPAdapter` with a `Retry` object, specifying the maximum number of retries and a backoff factor. This allows requests to be retried automatically in case of certain errors.

## Conclusion <a name="conclusion"></a>

Handling server errors when making HTTP requests is essential for building robust and reliable applications. By using the `requests` library and following the best practices discussed in this article, you can confidently handle server errors and provide a better user experience.