---
layout: post
title: "[python] Handling multipart/form-data in Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

When working with APIs that involve file uploads, you may come across the need to send a POST request with `multipart/form-data` content-type. The `multipart/form-data` format is commonly used for sending binary data, such as files, through HTTP requests.

Python's `requests` library provides an easy and convenient way to handle such requests. In this blog post, we will explore how to handle `multipart/form-data` content-type using Python Requests.

## Installing requests library

Before we dive into handling `multipart/form-data`, let's make sure we have the `requests` library installed. If you don't have it installed already, you can install it by running the following command:

```bash
pip install requests
```

## Uploading a file using multipart/form-data

To upload a file using `multipart/form-data`, we need to construct a request payload that includes the file to be uploaded. Here's an example of how you can upload a file using Python Requests:

```python
import requests

url = "https://api.example.com/upload"
file_path = "/path/to/file.png"

with open(file_path, "rb") as file:
    response = requests.post(url, files={"file": file})

print(response.status_code)
```

In the above example, we specify the URL of the API endpoint and the path to the file we want to upload. We then open the file in binary mode (`rb`), and pass it as a dictionary value to the `files` parameter of the `post` method. The key `"file"` in `files={"file": file}` represents the name of the field that the API expects to receive the file under.

Finally, we print the response status code to verify if the file upload was successful.

## Uploading multiple files

To upload multiple files using `multipart/form-data`, you can pass a list of files to the `files` parameter. Here's an example:

```python
import requests

url = "https://api.example.com/upload"
file_paths = ["/path/to/file1.png", "/path/to/file2.png"]

files = [("file", open(file_path, "rb")) for file_path in file_paths]

response = requests.post(url, files=files)

print(response.status_code)
```

In the above example, we iterate over a list of file paths and create a list of tuples using a list comprehension. Each tuple consists of a key-value pair, where the key `"file"` represents the field name and the value is the opened file in binary mode (`rb`).

## Sending additional form fields

In addition to uploading files, you may need to send additional form fields along with the file. You can do this by passing a dictionary as the `data` parameter in the `post` method. Here's an example:

```python
import requests

url = "https://api.example.com/upload"
file_path = "/path/to/file.png"

data = {
    "description": "Sample file",
    "category": "Images"
}

with open(file_path, "rb") as file:
    response = requests.post(url, files={"file": file}, data=data)

print(response.status_code)
```

In the above example, we define a `data` dictionary with additional form fields such as `"description"` and `"category"`. We pass this dictionary as the `data` parameter along with the file to the `post` method.

## Conclusion

Handling `multipart/form-data` in Python Requests is straightforward and convenient. By using the `files` parameter and optionally the `data` parameter, you can easily upload files and send additional form fields in your API requests.

Remember to handle any errors and check the response status code to ensure the successful completion of your file upload requests.

I hope this blog post helps you in working with `multipart/form-data` using Python Requests!