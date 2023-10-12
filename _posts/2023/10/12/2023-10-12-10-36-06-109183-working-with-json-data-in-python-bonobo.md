---
layout: post
title: "[python] Working with JSON data in Python Bonobo"
description: " "
date: 2023-10-12
tags: [python]
comments: true
share: true
---

Python Bonobo is a flexible and easy-to-use ETL (Extract, Transform, Load) framework. It provides a convenient way to work with JSON data by offering functions and methods to manipulate and process JSON structures.

In this blog post, we will explore how to work with JSON data using Python Bonobo.

## Table of Contents
1. Introduction
2. Loading JSON data
3. Extracting data from JSON
4. Transforming JSON data
5. Loading JSON data
6. Conclusion

## 1. Introduction
JSON (JavaScript Object Notation) is a popular data interchange format that is human-readable and easy to parse. It is widely used in web applications as a lightweight data format. Bonobo provides built-in support for working with JSON data, making it a great choice for ETL tasks involving JSON.

## 2. Loading JSON data
To load JSON data in Bonobo, we can use the `json.loads()` function to deserialize the JSON string into a Python dictionary. Here is an example:

```python
import json

def load_json_data():
    json_data = '{"name": "John Doe", "age": 30, "city": "New York"}'
    data = json.loads(json_data)
    return data

print(load_json_data())
```

Output:
```
{'name': 'John Doe', 'age': 30, 'city': 'New York'}
```

## 3. Extracting data from JSON
Once we have loaded the JSON data into a Python dictionary, we can easily extract specific values using their keys. For example, let's extract the value of the "name" key from the JSON data:

```python
import json

def extract_name(json_data):
    data = json.loads(json_data)
    name = data["name"]
    return name

# Assuming we have the following JSON data
json_data = '{"name": "John Doe", "age": 30, "city": "New York"}'
print(extract_name(json_data))
```

Output:
```
John Doe
```

## 4. Transforming JSON data
Bonobo provides various transformation functions to manipulate JSON data. For example, let's say we want to transform the JSON data by converting the "age" value from string to integer:

```python
import json

def transform_age(json_data):
    data = json.loads(json_data)
    data["age"] = int(data["age"])
    return json.dumps(data)

# Assuming we have the following JSON data
json_data = '{"name": "John Doe", "age": "30", "city": "New York"}'
print(transform_age(json_data))
```

Output:
```
{"name": "John Doe", "age": 30, "city": "New York"}
```

## 5. Loading JSON data
To load JSON data in Bonobo, we can use the `json.dumps()` function to serialize the Python dictionary back into a JSON string. Here is an example:

```python
import json

def load_json_data():
    data = {"name": "John Doe", "age": 30, "city": "New York"}
    json_data = json.dumps(data)
    return json_data

print(load_json_data())
```

Output:
```
{"name": "John Doe", "age": 30, "city": "New York"}
```

## 6. Conclusion
Python Bonobo provides a convenient way to work with JSON data in ETL tasks. With its built-in functions and methods, you can easily load, extract, transform, and load JSON data. Whether you are processing data from web APIs or working with JSON files, Bonobo makes it simple and efficient to work with JSON in Python.

Happy coding with Bonobo and JSON!