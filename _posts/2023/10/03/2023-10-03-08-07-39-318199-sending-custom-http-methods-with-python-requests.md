---
layout: post
title: "[python] Sending custom HTTP methods with Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

Python's `Requests` library provides a convenient way to send HTTP requests and interact with web services. Typically, you make requests using common HTTP methods like GET, POST, PUT, or DELETE. However, there may be situations where you need to send a custom HTTP method that is not supported by the library out of the box.

In this tutorial, we will explore how to send custom HTTP methods using Python Requests.

## Prerequisites

Make sure you have Python installed on your machine, along with the `Requests` library. You can install `Requests` using `pip`:

```
$ pip install requests
```

## Sending a custom HTTP method

By default, the `Requests` library supports the most commonly used HTTP methods, but if you need to send a custom method, you can do so by specifying the `method` parameter in the `request` function.

Here's an example of sending a custom HTTP method using `Requests`:

```python
import requests

# Define the custom method
custom_method = "MYMETHOD"

# Send the request with the custom method
response = requests.request(custom_method, url)
```

Replace `MYMETHOD` with the custom HTTP method you want to use and `url` with the URL you want to send the request to.

## Handling responses

Once you have sent the request with a custom method, you can handle the response as you would with any other request made using `Requests`. You can access the response status code, headers, and response content.

Here's an example of handling the response from a request with a custom method:

```python
import requests

# Define the custom method
custom_method = "MYMETHOD"

# Send the request with the custom method
response = requests.request(custom_method, url)

# Check the response status code
if response.status_code == 200:
    print("Request successful")
else:
    print("Request failed")

# Access the response content
content = response.content
```

## Conclusion

Python's `Requests` library offers a simple way to interact with web services by supporting common HTTP methods. However, when you need to send a custom HTTP method, you can use the `request` function along with the `method` parameter to achieve that. This flexibility allows you to work with APIs that require non-standard or custom HTTP methods.

Remember to handle the response as you would with any other request, by checking the status code and accessing the content if needed.

That's it! You now know how to send custom HTTP methods using Python Requests. Happy coding!