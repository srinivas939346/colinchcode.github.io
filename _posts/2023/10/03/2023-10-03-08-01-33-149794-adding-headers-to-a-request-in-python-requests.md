---
layout: post
title: "[python] Adding headers to a request in Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

When making HTTP requests using the Python `requests` library, you may need to include additional headers to provide more information to the server. These headers can be used for various purposes like authentication, specifying the content type, or controlling caching behavior. In this tutorial, we will explore how to add headers to a request in Python using `requests`.

## Overview of Headers in HTTP

Headers in HTTP are key-value pairs that provide additional information about the request or the response. They are included in the header section of the HTTP message and are used to transfer metadata between the client and the server.

Headers can contain information such as:

- Content-Type: specifies the media type of the request or response body
- User-Agent: provides information about the client making the request
- Authorization: used for authentication purposes
- Cache-Control: controls caching behavior
- and many more...

## Adding Headers using Python Requests

The `requests` module provides a simple and elegant interface for making HTTP requests in Python. To add headers to a request, you can make use of the `headers` parameter in the `requests` function. Let's see an example:

```python
import requests

# Define the headers
headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3',
    'Accept-Language': 'en-US,en;q=0.9',
    'Authorization': 'Bearer my_token'
}

# Make the request with headers
response = requests.get('https://api.example.com/resource', headers=headers)

# Process the response
print(response.status_code)
print(response.text)
```

In this example, we defined a dictionary variable `headers` that contains the headers we want to include in the request. The `User-Agent` header specifies the browser user agent string, which can be useful for some APIs. The `Accept-Language` header indicates the preferred language for the response. And finally, the `Authorization` header is used for authentication purposes, typically for APIs that require a token.

We then pass the `headers` variable to the `headers` parameter of the `requests.get` function to include the headers in the request. The `get` function sends an HTTP GET request to the specified URL and returns a `Response` object.

Finally, we can process the response as needed. In the example, we print the status code of the response and the response body.

## Conclusion

Adding headers to a request is a common requirement when working with HTTP APIs in Python. The `requests` library makes it simple and straightforward to include headers in your requests. Whether you need to specify custom headers, authentication tokens, or control caching behavior, the `headers` parameter of the `requests` function has got you covered. Happy coding!