---
layout: post
title: "[python] What is a Python dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

In a dictionary, each key is unique and is used to access its corresponding value. The keys can be of any immutable data type such as integers, strings, or tuples. The values can be of any data type, including other dictionaries.

To create a dictionary in Python, use curly braces `{}` and separate each key-value pair with a colon `:`. For example:

```python
my_dict = {"name": "John", "age": 30, "location": "New York"}
```

In the above example, "name", "age", and "location" are the keys, while "John", 30, and "New York" are the corresponding values.

You can access the values in a dictionary by using the keys. For example:

```python
print(my_dict["name"])  # Output: John
print(my_dict["age"])   # Output: 30
```

To modify the value of a key, simply assign a new value to it:

```python
my_dict["age"] = 32
print(my_dict["age"])   # Output: 32
```

Dictionaries in Python are incredibly useful for tasks like storing configuration settings, mapping data, and implementing lookup tables. They provide fast access to values based on their unique keys.

It's important to note that dictionaries are unordered, meaning that the order of the key-value pairs is not guaranteed. If you need to maintain the order of elements, you can use a `collections.OrderedDict`.