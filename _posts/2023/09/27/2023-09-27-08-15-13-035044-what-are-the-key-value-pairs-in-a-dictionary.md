---
layout: post
title: "[python] What are the key-value pairs in a dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

To create a dictionary in Python, you can use curly braces `{}` or the `dict()` constructor. For example:

```python
# Using curly braces
my_dict = {'key1': 'value1', 'key2': 'value2', 'key3': 'value3'}

# Using the dict() constructor
my_dict = dict(key1='value1', key2='value2', key3='value3')
```

In the above examples, we have created a dictionary with three key-value pairs. The keys (`key1`, `key2`, `key3`) are strings, and the values (`value1`, `value2`, `value3`) can be of any data type (string, integer, list, etc.).

To access the value associated with a specific key, you can use square brackets `[]` or the `get()` method. For example:

```python
# Accessing a value using square brackets
print(my_dict['key1'])  # Output: value1

# Accessing a value using get()
print(my_dict.get('key2'))  # Output: value2
```

You can also **update** the value of a specific key or **add** new key-value pairs to a dictionary using square brackets. For example:

```python
# Updating a value
my_dict['key1'] = 'new_value1'

# Adding a new key-value pair
my_dict['key4'] = 'value4'
```

To iterate over the keys or values of a dictionary, you can use a `for` loop with the `keys()` or `values()` method. For example:

```python
# Iterating over keys
for key in my_dict.keys():
    print(key)

# Iterating over values
for value in my_dict.values():
    print(value)
```

In summary, dictionaries in Python store data as key-value pairs, where each key is unique and maps to its respective value. They provide an efficient way to store, retrieve, and manipulate data in a flexible manner.