---
layout: post
title: "[python] Handling URL encoding in Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

URL encoding, also known as percent-encoding, is a way to represent special characters in a URL by replacing them with their corresponding ASCII hexadecimal value. When sending requests using Python's `requests` library, it is important to properly handle URL encoding to ensure that the URLs are correctly formatted and can be understood by the server.

In this article, we will explore how to handle URL encoding in Python Requests and demonstrate some commonly used techniques.

## Understanding URL encoding

URL encoding is used to encode special characters that either have a special meaning in the URL syntax or do not conform to URL format rules. For example, spaces are not allowed in URLs, so they need to be encoded as `%20`. Other common examples include `?` being encoded as `%3F` and `&` being encoded as `%26`.

## Handling URL encoding in Python Requests

Python's `requests` library automatically handles proper URL encoding for you, so you don't need to manually encode the URLs. You can simply pass the URL as a string to the `requests.get()` or `requests.post()` method, and it will take care of the encoding.

Here's an example of how to make a GET request using `requests` with an encoded URL:

```python
import requests

url = "http://example.com/search?q=python requests"
response = requests.get(url)

print(response.text)
```

In the above example, the space in the search query `"python requests"` is automatically encoded as `%20` by the `requests` library. The encoded URL, `http://example.com/search?q=python%20requests`, is sent to the server.

## URL encoding query parameters

When sending a request with query parameters, you can pass them as a dictionary to the `params` parameter of the `requests.get()` or `requests.post()` method. The `requests` library will handle the URL encoding of the query parameters for you.

```python
import requests

url = "http://example.com/search"
params = {"q": "python requests"}

response = requests.get(url, params=params)

print(response.text)
```

In this example, the `params` dictionary is automatically URL encoded by `requests`, resulting in the URL `http://example.com/search?q=python%20requests`.

## Custom URL encoding

If you need to manually encode a URL or a specific part of a URL, you can use the `urllib.parse.quote()` function from Python's standard library.

```python
import requests
import urllib.parse

url = "http://example.com/search"
query = "python requests"

encoded_query = urllib.parse.quote(query)
encoded_url = f"{url}?q={encoded_query}"

response = requests.get(encoded_url)

print(response.text)
```

In this example, we manually encode the query parameter `"python requests"` using `urllib.parse.quote()`. The encoded query is then added to the URL by concatenating it.

## Conclusion

Handling URL encoding is essential when working with URLs in Python Requests. By allowing the `requests` library to handle the URL encoding automatically, you can focus on building your requests without worrying about the specifics of URL encoding. In cases where you need more control, Python provides the `urllib.parse` module for manual URL encoding.