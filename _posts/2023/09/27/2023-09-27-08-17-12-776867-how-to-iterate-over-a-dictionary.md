---
layout: post
title: "[python] How to iterate over a dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

Keywords: Python, dictionary, iteration, loop

---

Python provides various ways to iterate over a dictionary and perform operations on its key-value pairs. In this blog post, we will explore different methods for iterating over dictionaries in Python.

Method 1: Using a For Loop

```python
my_dict = {'name': 'John', 'age': 30, 'country': 'USA'}

for key in my_dict:
    print(key, ':', my_dict[key])
```

Explanation: In this method, we use a for loop to iterate over the keys of the dictionary. For each key, we can access its corresponding value using square brackets notation (`my_dict[key]`).

Method 2: Using the items() Method

```python
my_dict = {'name': 'John', 'age': 30, 'country': 'USA'}

for key, value in my_dict.items():
    print(key, ':', value)
```

Explanation: The `items()` method returns a view object that contains key-value tuples of the dictionary. By looping over this view object, we can access both the keys and values directly.

Method 3: Using the keys() Method

```python
my_dict = {'name': 'John', 'age': 30, 'country': 'USA'}

for key in my_dict.keys():
    print(key, ':', my_dict[key])
```

Explanation: The `keys()` method returns a view object that contains the keys of the dictionary. By looping over this view object, we can extract the keys and access their corresponding values from the dictionary.

Method 4: Using the values() Method

```python
my_dict = {'name': 'John', 'age': 30, 'country': 'USA'}

for value in my_dict.values():
    print(value)
```

Explanation: The `values()` method returns a view object that contains the values of the dictionary. By looping over this view object, we can directly access the values without requiring the keys.

These are the four commonly used methods for iterating over dictionaries in Python. Choose the appropriate method based on your requirements and use case.

Remember, dictionaries are unordered collections, so the order of iteration might not be consistent.