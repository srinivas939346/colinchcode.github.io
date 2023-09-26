---
layout: post
title: "[python] What is a nested dictionary in Python?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

In Python, a nested dictionary is a dictionary that contains another dictionary as its value. This allows for a more complex and structured way of organizing data. Nested dictionaries are often used to represent data in a hierarchical manner, where each level of the hierarchy is represented by a dictionary.

## Creating a Nested Dictionary

To create a nested dictionary in Python, you can simply assign a dictionary as the value to a key in another dictionary. Here's an example:

```python
# Creating a nested dictionary
student = {
  "name": "John Doe",
  "age": 21,
  "grades": {
    "math": 90,
    "science": 85,
    "history": 95
  }
}
```

In this example, the `student` dictionary contains three key-value pairs. The `grades` key has a dictionary as its value, representing the grades in different subjects.

## Accessing Values in a Nested Dictionary

You can access values in a nested dictionary by using multiple indexing. Here's how you can do it:

```python
# Accessing values in a nested dictionary
print(student["name"])  # Output: John Doe
print(student["grades"]["math"])  # Output: 90
```

In this code snippet, we access the value of the `name` key using the single indexing operator `[]`. To access the `math` grade, we use multiple indexing with `["grades"]["math"]`.

## Modifying Values in a Nested Dictionary

To modify the values in a nested dictionary, you can use the same indexing syntax as when accessing the values. Here's an example:

```python
# Modifying values in a nested dictionary
student["grades"]["science"] = 90
print(student["grades"]["science"])  # Output: 90
```

In this example, we modify the value of the `science` key under the `grades` dictionary to 90.

## Conclusion

Nested dictionaries in Python provide a convenient way to organize and access structured data. By using dictionaries as values, you can create complex hierarchies that represent relationships between different data elements. This can be useful in various scenarios, such as representing JSON data or organizing complex configurations.