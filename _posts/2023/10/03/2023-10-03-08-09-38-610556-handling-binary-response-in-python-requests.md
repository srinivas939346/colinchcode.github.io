---
layout: post
title: "[python] Handling binary response in Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

When working with APIs or web scraping, sometimes you might encounter endpoints that return binary data instead of plain text or JSON. In Python, the `requests` library is commonly used for making HTTP requests, but it automatically decodes the response content as text by default. So, how do you handle binary responses in `requests`?

## Sending a binary request

Before we delve into handling binary responses, let's quickly go over how to send a binary request using `requests`. Normally, when making requests using `requests.get()` or `requests.post()`, you provide a URL and optional parameters. To send a binary request, you can simply pass the `bytes` object as the request body using the `data` parameter.

Here's an example of how to send a binary POST request using `requests`:

```python
import requests

binary_data = b'\x01\x02\x03\x04'  # Binary data as bytes

response = requests.post('https://example.com/api', data=binary_data)
```

In the above example, we create a `bytes` object `binary_data` and pass it as the `data` parameter in the `post()` method. This will send a binary POST request to the specified URL.

## Handling binary response

By default, `requests` will decode the response content as Unicode text using the encoding specified in the HTTP response headers. However, when dealing with binary responses, you need to access the raw response data without any decoding.

To access the raw binary response content, you can use the `response.content` attribute. This attribute returns the response content as `bytes`. You can then process the binary data based on your specific use case.

Here's an example of how to handle binary response in `requests`:

```python
import requests

response = requests.get('https://example.com/image.jpg')

if response.status_code == 200:
    with open('image.jpg', 'wb') as file:
        file.write(response.content)
        print("Image downloaded successfully!")
else:
    print(f"Failed to download image. Status code: {response.status_code}")
```

In the above example, we send a GET request to an image URL and save the binary response content to a file named `image.jpg`. We use the `response.content` attribute to get the binary data and write it to the file in binary mode (`'wb'`).

## Conclusion

Handling binary responses in Python `requests` is straightforward. You can send binary requests by passing a `bytes` object as the request body. To handle binary responses, you can access the raw binary data using the `response.content` attribute.

Remember to handle errors appropriately and ensure that you have necessary permissions and rights to download and process binary data from the target endpoint.