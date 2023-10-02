---
layout: post
title: "[python] Using proxies with Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

When making HTTP requests in Python using the `requests` library, you can also make use of proxies to route your requests through a different IP address. Proxies can be useful for a variety of purposes such as scraping websites, bypassing geographic restrictions, or ensuring anonymity.

In this tutorial, we will explore how to use proxies with Python Requests to make HTTP requests through a proxy server.

## Prerequisites
Before we begin, make sure you have Python installed on your machine along with the `requests` library. If you don't have the `requests` library installed, you can install it using `pip`.

```python
pip install requests
```

## Using Proxies in Python Requests
To use a proxy server with Python Requests, you need to pass the `proxies` parameter to the request methods. The `proxies` parameter expects a dictionary where the keys represent the protocol (http or https) and the values are the proxy URLs.

Let's start by creating a simple GET request using a proxy server:

```python
import requests

# Define the proxy server URL
proxy_url = 'http://your-proxy-url'

# Define the URL you want to request
url = 'http://example.com'

# Define the proxy dictionary
proxies = {
    'http': proxy_url,
    'https': proxy_url
}

# Make the request using the proxy
response = requests.get(url, proxies=proxies)

# Print the response content
print(response.content)
```

In the code above, we have defined a proxy URL and a target URL. We then create a dictionary with the proxy URL and pass it to the `proxies` parameter of the `requests.get()` method. The response is then printed to the console.

## Proxy Authentication
If your proxy server requires authentication, you can pass additional parameters to the `proxies` dictionary. Here's how you can specify the username and password for proxy authentication:

```python
import requests

# Define the proxy server URL
proxy_url = 'http://your-proxy-url'

# Define the URL you want to request
url = 'http://example.com'

# Define the proxy dictionary with authentication
proxies = {
    'http': 'http://username:password@' + proxy_url,
    'https': 'http://username:password@' + proxy_url
}

# Make the request using the proxy with authentication
response = requests.get(url, proxies=proxies)

# Print the response content
print(response.content)
```

In the code above, we include the username and password in the proxy URL using the format `http://username:password@proxy_url`.

## Conclusion
Using proxies with Python Requests allows you to route your HTTP requests through different IP addresses. This can be useful for various purposes such as web scraping, bypassing restrictions, or maintaining anonymity. By leveraging the `proxies` parameter in Python Requests, you can easily integrate proxy functionality into your applications.