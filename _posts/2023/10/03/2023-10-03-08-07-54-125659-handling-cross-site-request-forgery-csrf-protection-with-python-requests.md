---
layout: post
title: "[python] Handling cross-site request forgery (CSRF) protection with Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

When working with web applications that require user authentication and session management, it's essential to protect against cross-site request forgery (CSRF) attacks. CSRF attacks occur when an attacker tricks a user into performing unintended actions on a web application by exploiting the user's authenticated session.

In this blog post, we'll explore how to handle CSRF protection when using the Python Requests library, one of the most popular libraries for making HTTP requests in Python.

## Table of Contents
- [What is CSRF protection?](#what-is-csrf-protection)
- [How CSRF protection works](#how-csrf-protection-works)
- [Handling CSRF tokens in Python Requests](#handling-csrf-tokens-in-python-requests)
  - [Extracting the CSRF token](#extracting-the-csrf-token)
  - [Including the token in subsequent requests](#including-the-token-in-subsequent-requests)
- [Conclusion](#conclusion)

## What is CSRF protection?

Cross-site request forgery (CSRF or XSRF) is a type of web security vulnerability where an attacker exploits the trust of a website in a user's browser. CSRF attacks occur when an authenticated user inadvertently performs an action on a website without their consent or knowledge.

To prevent CSRF attacks, web applications often employ CSRF protection mechanisms that involve adding and validating tokens on each request.

## How CSRF protection works

When a user authenticates with a web application, the server generates a unique CSRF token and associates it with the user's session. The token is usually embedded in the web application's form or as a header in subsequent requests. Whenever a user submits a form or performs an action, the application verifies the presence and validity of the CSRF token.

## Handling CSRF tokens in Python Requests

To handle CSRF protection when making requests with Python Requests, you need to extract the CSRF token from the server's response and include it in subsequent requests.

### Extracting the CSRF token

The process of extracting the CSRF token depends on the specific web application you're interacting with. In some cases, the token may be present as a hidden input field within a form, while in others, it might be included in a custom header.

Here's an example of how to extract a CSRF token from an HTML form using the BeautifulSoup library:

```python
import requests
from bs4 import BeautifulSoup

# Make a request to the login page
response = requests.get("https://example.com/login")

# Parse the HTML response using BeautifulSoup
soup = BeautifulSoup(response.text, "html.parser")

# Find the CSRF token input field
csrf_token = soup.find("input", attrs={"name": "csrf_token"})["value"]
```

In the example above, we use `requests` library to make a GET request to the login page. Then, we parse the HTML response using `BeautifulSoup` and extract the value of the CSRF token input field.

### Including the token in subsequent requests

Once you have extracted the CSRF token, you need to include it in the headers or the form data of subsequent requests. The specific method of inclusion depends on how the web application verifies the token.

Here's an example of including the CSRF token in the headers of a POST request:

```python
import requests

# Assuming the csrf_token variable contains the extracted CSRF token
csrf_token = "<csrf_token_value>"

headers = {
    "X-CSRF-Token": csrf_token,
    "Content-Type": "application/json"
}

data = {
    "name": "John Doe",
    "email": "john.doe@example.com"
}

response = requests.post("https://example.com/api/users", headers=headers, json=data)
```

In the example above, we include the CSRF token in the `X-CSRF-Token` header of the POST request. Additionally, we set the `Content-Type` header as `"application/json"` to indicate that the request body is in JSON format.

## Conclusion

CSRF protection is an important aspect of web application security. By incorporating proper CSRF protection mechanisms into your Python Requests code, you can help safeguard against potential attacks. Remember to extract the CSRF token from the server's response and include it in subsequent requests to ensure proper validation.

With Python Requests, handling CSRF protection is straightforward, thanks to its flexibility in setting headers and form data.

Happy coding and stay secure!