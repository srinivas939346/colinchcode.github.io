---
layout: post
title: "[python] Sending a PUT request using Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

In this blog post, we will learn how to send a PUT request using the Python Requests library. The Requests library is a popular choice for making HTTP requests in Python due to its simplicity and intuitive API.

## Table of Contents

1. Introduction
2. Creating a PUT request
3. Adding request headers
4. Sending request data
5. Handling response

## 1. Introduction

The HTTP PUT method is used to update an existing resource on a server. It requires the client to send the updated representation of the resource in the request payload. In this case, we will be using the Python Requests library to make the PUT request.

## 2. Creating a PUT request

To create a PUT request, we need to use the `requests.put()` method and provide the URL of the resource we want to update. Here's an example:

```python
import requests

url = 'https://api.example.com/resource/123'
response = requests.put(url)
```

In the above code snippet, we import the Requests library and create a PUT request using the `requests.put()` method. We pass the URL of the resource we want to update to the method.

## 3. Adding request headers

Headers are used to provide additional information about the request or to specify the format of the request payload. We can add custom headers to our PUT request using the `headers` parameter of the `requests.put()` method. Here's an example:

```python
import requests

url = 'https://api.example.com/resource/123'
headers = {'Content-Type': 'application/json'}
response = requests.put(url, headers=headers)
```

In the above code snippet, we add a custom header `'Content-Type'` with a value of `'application/json'`. This header specifies that the request payload will be in JSON format.

## 4. Sending request data

To send data in the request payload, we can pass a dictionary of key-value pairs using the `data` parameter of the `requests.put()` method. Here's an example:

```python
import requests

url = 'https://api.example.com/resource/123'
data = {'name': 'John Doe', 'age': 30}
response = requests.put(url, data=data)
```

In the above code snippet, we pass a dictionary with the keys `'name'` and `'age'` as the request data. The server can then use this data to update the resource.

## 5. Handling response

After sending the PUT request, we receive a response from the server. We can access various attributes of the response, such as status code, content, headers, etc. Here's an example:

```python
import requests

url = 'https://api.example.com/resource/123'
response = requests.put(url)
content = response.content
status_code = response.status_code

print(f'Response content: {content}')
print(f'Status code: {status_code}')
```

In the above code snippet, we print the content of the response using `response.content` and the status code using `response.status_code`.

That's it! Now you know how to send a PUT request using Python Requests. The library provides a simple and powerful way to interact with HTTP resources and handle the responses. You can further explore the Requests library's documentation for more advanced features and functionalities.

Thank you for reading!