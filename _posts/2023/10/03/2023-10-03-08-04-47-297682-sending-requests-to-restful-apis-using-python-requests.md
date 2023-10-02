---
layout: post
title: "[python] Sending requests to RESTful APIs using Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to send requests to RESTful APIs using the Python Requests library. 

## Table of Contents

- [Introduction](#introduction)
- [Installing the requests library](#installing-the-requests-library)
- [Making GET requests](#making-get-requests)
- [Making POST requests](#making-post-requests)
- [Making PUT and DELETE requests](#making-put-and-delete-requests)
- [Conclusion](#conclusion)

## Introduction

When interacting with RESTful APIs, it is essential to send HTTP requests to retrieve and manipulate data. Python provides the `requests` library, a powerful and user-friendly tool for making HTTP requests. 

## Installing the requests library

Before we get started, we need to install the requests library. Open your terminal and run the following command:

```shell
pip install requests
```

## Making GET requests

To make a GET request, we can use the `requests.get()` method. Let's make a simple GET request to retrieve information from a public API. Here's an example:

```python
import requests

response = requests.get("https://api.example.com/data")
data = response.json()
print(data)
```

In this example, we make a GET request to the specified URL and store the response in the `response` variable. We can then access the response data using the `json()` method, which returns a Python dictionary. Finally, we print the data to the console.

## Making POST requests

To make a POST request, we can use the `requests.post()` method. Let's say we want to send some data to a server using a POST request. Here's an example:

```python
import requests

data = {
    "name": "John Doe",
    "email": "johndoe@example.com"
}

response = requests.post("https://api.example.com/users", json=data)
print(response.status_code)
```

In this example, we create a Python dictionary `data` containing the user's name and email. We then make a POST request to the `/users` endpoint, sending the data as JSON using the `json` parameter. The server will process the request and return a response. We can access the status code of the response using the `status_code` attribute.

## Making PUT and DELETE requests

To make PUT or DELETE requests, we can use the `requests.put()` and `requests.delete()` methods, respectively. Let's see an example of making a PUT request to update a resource:

```python
import requests

data = {
    "name": "Updated Name",
    "email": "updated_email@example.com"
}

response = requests.put("https://api.example.com/users/1", json=data)
print(response.status_code)
```

In this example, we make a PUT request to the `/users/1` endpoint, updating the user's name and email. 

Similarly, we can make DELETE requests using the `requests.delete()` method:

```python
import requests

response = requests.delete("https://api.example.com/users/1")
print(response.status_code)
```

This example demonstrates how to make a DELETE request to delete a specific resource.

## Conclusion

In this article, we have explored how to send requests to RESTful APIs using the Python Requests library. We have covered making GET, POST, PUT, and DELETE requests and accessing the response data. The requests library provides a simple yet robust way to interact with APIs, making it a valuable tool for any Python developer working with web services.