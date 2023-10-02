---
layout: post
title: "[python] Parsing XML response using Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

When working with REST APIs, it's common to receive responses in XML format. Python's `requests` library makes it easy to send HTTP requests and handle the responses. In this tutorial, we'll explore how to parse an XML response using `requests`.

## Prerequisites

To follow along, make sure you have the following installed:

- Python (version 3.x)
- Requests library (`pip install requests`)

## Sending a request

First, let's start by sending a request to a API endpoint that returns an XML response. We'll be using the `GET` method in this example:

```python
import requests

url = "https://api.example.com/data"
response = requests.get(url)

if response.status_code == 200:
    xml_response = response.content
    # The response is now stored in `xml_response`
else:
    print("Request failed with status code:", response.status_code)
```

In the code above, we import the `requests` library and send a `GET` request to the specified URL. We then check the status code of the response to ensure the request was successful. If it was, we store the response content in `xml_response`.

## Parsing the XML response

To parse the XML response, we can use Python's built-in `xml.etree.ElementTree` module. This module provides a simple and efficient way to parse XML data.

```python
import xml.etree.ElementTree as ET

# Assuming `xml_response` holds the XML content from the previous code snippet

# Parse the XML and get the root element
root = ET.fromstring(xml_response)

# Accessing XML elements and attributes
for child in root:
    print(child.tag, child.attrib)
```

In the code above, we import the `xml.etree.ElementTree` module and parse the XML content using the `fromstring` function. This returns the root element of the XML structure.

We can then iterate over the child elements of the root element and access their tags and attributes. Feel free to modify this code to fit your specific XML structure.

## Conclusion

Using Python's `requests` library in combination with `xml.etree.ElementTree`, we can easily send HTTP requests and parse XML responses. This allows us to work with REST APIs that return XML data in an efficient manner.

Remember to handle error cases appropriately and ensure that the XML response follows the expected structure for smooth parsing. Happy coding!