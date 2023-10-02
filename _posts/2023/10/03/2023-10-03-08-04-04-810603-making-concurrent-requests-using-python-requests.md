---
layout: post
title: "[python] Making concurrent requests using Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

In this blog post, we'll explore how to make concurrent requests using the `requests` library in Python. The `requests` library is widely used for sending HTTP requests and handling responses in a simple and intuitive way. However, making sequential requests can be time-consuming.

To overcome this limitation, we can use `concurrent.futures` module from Python's standard library, which allows us to parallelize the execution of requests. Using `concurrent.futures`, we can easily make multiple requests concurrently and greatly improve the performance of our code.

## What is concurrent programming?

Concurrent programming is a programming paradigm that allows multiple tasks to be executed concurrently, rather than sequentially. By running tasks concurrently, we can achieve better performance and make efficient use of available resources.

## Getting started

To get started, we need to install the `requests` library if it's not already installed. Open your terminal or command prompt and run the following command:

```
pip install requests
```

Once we have `requests` installed, we can proceed with the implementation.

## Using concurrent.futures for concurrent requests

To make concurrent requests, we'll use the `ThreadPoolExecutor` class from the `concurrent.futures` module. It provides a simple interface for running multiple tasks concurrently in a pool of worker threads.

Here's an example that demonstrates how to use `ThreadPoolExecutor` to make concurrent requests:

```python
import requests
from concurrent.futures import ThreadPoolExecutor

urls = [
    'https://example.com',
    'https://google.com',
    'https://github.com',
    'https://stackoverflow.com'
]

def fetch_url(url):
    response = requests.get(url)
    print(f'Response from {url}: {response.status_code}')

# Create a ThreadPoolExecutor with 4 worker threads
with ThreadPoolExecutor(max_workers=4) as executor:
    # Submit the fetch_url function to the executor for each URL
    futures = [executor.submit(fetch_url, url) for url in urls]

    # Wait for all the tasks to complete
    for future in futures:
        future.result()
```

In this example, we define a list of URLs that we want to fetch. We then define the `fetch_url` function, which takes a URL as a parameter and sends a GET request to that URL using `requests.get()`. Finally, we create a `ThreadPoolExecutor` with 4 worker threads and use it to submit the `fetch_url` function for each URL. We wait for all the tasks to complete by calling the `result()` method on each future.

By using `ThreadPoolExecutor`, the requests will be made concurrently, allowing us to fetch multiple URLs at the same time. This can significantly speed up the execution of our program, especially when dealing with a large number of requests.

## Conclusion

In this blog post, we've seen how to make concurrent requests using Python's `requests` library and `concurrent.futures` module. By using `ThreadPoolExecutor`, we can easily parallelize the execution of requests and achieve better performance in our code. So the next time you need to make multiple requests, consider using concurrent programming to speed up your code.