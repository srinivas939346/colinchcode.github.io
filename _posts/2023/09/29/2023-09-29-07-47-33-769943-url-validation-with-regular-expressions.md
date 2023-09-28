---
layout: post
title: "[python] URL validation with regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to validate URLs using regular expressions in Python. URL validation is an important task in web development as it ensures that the URLs entered by users are in the correct format.

### What is a URL?

Before we dive into URL validation, let's understand what a URL is. A URL, or Uniform Resource Locator, is a string of characters that provides a way to access resources on the internet. It typically consists of a protocol, followed by the domain name or IP address of the server, and may include additional path and query parameters.

### Regular expressions for URL validation

Regular expressions are a powerful tool for pattern matching in strings. They can be used to define a pattern for URL validation as well. Here's an example regular expression in Python that can be used to validate URLs:

```python
import re

def validate_url(url):
    pattern = re.compile(r'^https?://(?:[a-zA-Z0-9-]+\.)+[a-zA-Z]{2,}(?:/[^\s]*)?$')
    return bool(pattern.match(url))
```

In the code above, we define a function `validate_url` that takes a URL as input and uses the regular expression pattern to check if the URL is valid. The pattern matches URLs starting with either `http://` or `https://`, followed by the domain name, and optionally followed by a path.

### Example usage

Let's see some examples of how this URL validation can be used:

```python
valid_urls = [
    "https://www.example.com",
    "http://example.com/path/to/resource",
    "https://subdomain.example.com/page.html",
]

invalid_urls = [
    "www.example.com",
    "http://example",
    "https://",
]

for url in valid_urls:
    if validate_url(url):
        print(f"{url} is a valid URL")
    else:
        print(f"{url} is not a valid URL")

for url in invalid_urls:
    if validate_url(url):
        print(f"{url} is a valid URL")
    else:
        print(f"{url} is not a valid URL")
```

In the example code, we have a list of valid and invalid URLs. We iterate over each URL, calling the `validate_url` function to check if it is valid or not.

### Conclusion

Regular expressions provide a powerful and flexible way to validate URLs. By using regular expressions, we can ensure that the URLs entered by users are in the correct format. In this blog post, we learned how to use a regular expression in Python to validate URLs.