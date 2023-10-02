---
layout: post
title: "[python] Sending and receiving cookies with Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

When making HTTP requests using the `requests` library in Python, you may often need to send or receive cookies for session management and other purposes. In this tutorial, we will explore how to send and receive cookies using `requests`.

**Table of Contents**
- [Sending Cookies](#sending-cookies)
- [Receiving Cookies](#receiving-cookies)
- [Conclusion](#conclusion)

## Sending Cookies

To send cookies with your HTTP requests, you can use the `cookies` parameter of the `requests` library. This parameter allows you to pass a `dict` object containing the cookies.

Here's an example of sending cookies:

```python
import requests

cookies = {'cookie-name': 'cookie-value'}

response = requests.get('https://example.com', cookies=cookies)

```

In the above example, we create a `dict` object `cookies` that contains the cookie name and value. We then pass this `cookies` object as the value for the `cookies` parameter of `requests.get()` method. This will send the cookies along with the request.

If you have multiple cookies to send, you can add them to the `cookies` `dict` object:

```python
cookies = {'cookie1': 'value1', 'cookie2': 'value2'}
```

## Receiving Cookies

When making a request to a server, it can send back cookies in the response header. To access the cookies received in the response, you can use the `cookies` attribute of the `Response` object.

Here's an example of receiving cookies:

```python
import requests

response = requests.get('https://example.com')

cookies = response.cookies

for cookie in cookies:
    print(cookie.name, cookie.value)
```

In the above example, we make a GET request to `https://example.com`. The `response.cookies` attribute returns a `RequestsCookieJar` object containing all the cookies received in the response. We can iterate over this object to access the name and value of each cookie.

## Conclusion

Sending and receiving cookies with `requests` is quite simple. You can use the `cookies` parameter to send cookies with your requests and access the received cookies using the `response.cookies` attribute. Cookies are an essential part of managing sessions and retaining user information, so understanding how to handle them using `requests` is important for web scraping, automated testing, and various other tasks.