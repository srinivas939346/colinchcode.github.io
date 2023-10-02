---
layout: post
title: "[python] Handling cookies with Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

When working with web APIs or scraping web data, you often need to handle cookies. Cookies allow servers to recognize and remember the stateful information of a client.

In this post, we will explore how to handle cookies using the popular Python library `requests`.

## Table of Contents
- [Introduction to Cookies](#introduction-to-cookies)
- [Sending Cookies](#sending-cookies)
- [Receiving Cookies](#receiving-cookies)
- [Session Objects](#session-objects)
- [Conclusion](#conclusion)

## Introduction to Cookies

Cookies are small pieces of data sent from a website and stored on the user's computer by the browser. They are mainly used for session management, tracking user behavior, and personalization.

Each cookie contains several attributes, including the name, value, domain, path, expiration, and whether it is secure or not.

## Sending Cookies

To send cookies in a request using `requests`, you can pass a dictionary containing the cookie data to the `cookies` parameter of the request methods.

Here's an example that sends cookies in a GET request:

```python
import requests

url = 'https://example.com'
cookies = {'session_id': '12345', 'language': 'en'}

response = requests.get(url, cookies=cookies)

print(response.text)
```

In the above code, we create a dictionary `cookies` with key-value pairs representing the cookie names and values. We then pass this `cookies` dictionary to the `cookies` parameter of the `get` request.

## Receiving Cookies

When making a request with `requests`, it automatically handles the receiving of cookies, and you can access them using the `cookies` attribute of the response object.

Here's an example of receiving cookies in a response:

```python
import requests

url = 'https://example.com'

response = requests.get(url)

cookies = response.cookies

for cookie in cookies:
    print(cookie.name, cookie.value)
```

In the above code, we make a GET request to the URL and access the received cookies using the `cookies` attribute of the response object. We can then iterate over the cookies and access their attributes like `name` and `value`.

## Session Objects

`requests` also provides a `Session` object that can be used to persist certain parameters across multiple requests, including cookies.

Here's an example of using a `Session` object to persist cookies:

```python
import requests

url = 'https://example.com'
cookies = {'session_id': '12345', 'language': 'en'}

session = requests.Session()
session.cookies.update(cookies)

response = session.get(url)

print(response.text)
```

In the above code, we create a `Session` object and update its cookies using the `update` method. Then, we use the `get` method of the `Session` object to make a request.

Using a `Session` object is beneficial when you need to make multiple requests, and you want to persist the cookies and other parameters across those requests.

## Conclusion

Handling cookies with `requests` is straightforward and flexible. You can easily send and receive cookies using the `cookies` parameter of the request methods or by using a `Session` object. Understanding how to handle cookies is crucial when interacting with web APIs or scraping web data.

Remember to be mindful of security aspects when dealing with sensitive information stored in cookies and ensure you handle them securely.