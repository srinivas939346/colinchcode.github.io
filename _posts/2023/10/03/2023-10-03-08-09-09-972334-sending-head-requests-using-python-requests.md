---
layout: post
title: "[python] Sending HEAD requests using Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

When working with HTTP requests in Python, the `requests` library is commonly used. It provides a simple and elegant way to make HTTP requests and handle the responses. In some cases, you may only need to retrieve the headers of a response without downloading the entire response body. For such scenarios, you can use the `HEAD` request method.

In this tutorial, we'll explore how to send `HEAD` requests using the `requests` library in Python.

## Prerequisites
To follow along with this tutorial, make sure you have the following:

- Python installed on your machine
- `requests` library installed. You can install it using pip:
```shell
$ pip install requests
```

## Sending HEAD Requests
The `HEAD` method is similar to the `GET` method, but it only retrieves the headers of the response and not the response body. It can be useful when you need to check the status of a resource, retrieve specific headers, or retrieve metadata about a file or webpage.

Here's a basic example that shows how to use `requests` to send a `HEAD` request:

```python
import requests

# Define the URL you want to send a HEAD request to
url = "https://www.example.com/"

# Send the HEAD request
response = requests.head(url)

# Print the response status code and headers
print(f"Status Code: {response.status_code}")
print("Headers:")
for header, value in response.headers.items():
    print(f"{header}: {value}")
```

In the above code, we import the `requests` library and define the URL we want to send a `HEAD` request to. We then use the `head()` method from the `requests` library to send the `HEAD` request. The response object contains the status code and headers of the response.

We can access the response status code using `response.status_code` and iterate over the `response.headers` to print all the headers.

## Conclusion
Sending `HEAD` requests using the `requests` library in Python is very straightforward. It allows you to retrieve only the headers of a response without downloading the entire response body. This can be useful when you need to check the status of a resource or retrieve specific headers or metadata.