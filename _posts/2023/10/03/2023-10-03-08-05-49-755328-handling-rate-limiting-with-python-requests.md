---
layout: post
title: "[python] Handling rate limiting with Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

When working with APIs that have rate limits, it is essential to handle the rate limiting properly to ensure the best usage of the API without hitting any limitations. In this blog post, we will explore how to handle rate limiting using the Python Requests library.

## What is Rate Limiting?

Rate limiting is a technique used by APIs to control the number of requests a client can make in a given time window. APIs impose rate limits to protect their infrastructure from abuse, ensure fair usage for all clients, and maintain the overall quality of service.

## Python Requests Library

Requests is one of the most popular HTTP libraries for Python. It provides a convenient way to send HTTP requests and handle the response. You can install Requests using pip:

```python
pip install requests
```

## Identifying Rate Limiting Headers

Before we can handle rate limiting, we need to know how to identify the relevant rate limiting headers in the API response. The common rate limiting headers are:

- **X-RateLimit-Limit**: The maximum number of requests allowed in a specific time window.
- **X-RateLimit-Remaining**: The number of remaining requests available in the current time window.
- **X-RateLimit-Reset**: The timestamp when the rate limit will reset.

```
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 50
X-RateLimit-Reset: 1619712000
```

## Implementing Rate Limiting with Requests

To handle rate limiting with Requests, we need to extract the rate limiting headers from the API response and wait for the rate limit reset time if necessary. Here's an example implementation:

```python
import requests
import time

def make_request(url):
    response = requests.get(url)
    
    if 'X-RateLimit-Limit' in response.headers:
        limit = int(response.headers['X-RateLimit-Limit'])
        remaining = int(response.headers['X-RateLimit-Remaining'])
        reset = int(response.headers['X-RateLimit-Reset'])
        
        if remaining == 0:  # Rate limit exceeded
            wait_time = reset - time.time() + 1  # Add 1 second buffer
            time.sleep(wait_time)
            return make_request(url)  # Retry the request
            
    return response

# Usage example
response = make_request('https://api.example.com/endpoint')
print(response.json())
```

In the `make_request` function, we check if the rate limiting headers are present in the response. If the remaining requests are 0, we calculate the wait time until the rate limit resets and sleep for that duration. After waiting, we retry the request using recursion.

## Summary

Handling rate limiting is crucial when working with APIs. By understanding the rate limiting headers in the API response and implementing proper handling using the Python Requests library, we can effectively manage the rate limits and ensure smooth API interactions.