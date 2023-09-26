---
layout: post
title: "[python] How to copy a dictionary in Python?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

In Python, dictionaries are mutable objects that store key-value pairs. There are multiple ways to make a copy of a dictionary, each with its own advantages and use cases.

### Method 1: Using the copy() method

The `copy()` method is a built-in method for dictionaries in Python that creates a shallow copy of the dictionary.

```python
original_dict = {'a': 1, 'b': 2, 'c': 3}

# Create a shallow copy using copy() method
new_dict = original_dict.copy()

# Modify the original dictionary
original_dict['a'] = 10

# Print both dictionaries
print("Original Dictionary:", original_dict)
print("Copied Dictionary:", new_dict)
```

This will output:
```
Original Dictionary: {'a': 10, 'b': 2, 'c': 3}
Copied Dictionary: {'a': 1, 'b': 2, 'c': 3}
```

Advantages of `copy()` method:
- It creates a new dictionary object with a separate memory location, ensuring that modifications to one dictionary do not affect the other.
- It only creates a shallow copy, which means that any mutable objects within the dictionary will still reference the same memory location.

### Method 2: Using the dict() constructor

Another way to copy a dictionary is by using the `dict()` constructor. This method also creates a shallow copy of the dictionary.

```python
original_dict = {'a': 1, 'b': 2, 'c': 3}

# Create a shallow copy using dict() constructor
new_dict = dict(original_dict)

# Modify the original dictionary
original_dict['a'] = 10

# Print both dictionaries
print("Original Dictionary:", original_dict)
print("Copied Dictionary:", new_dict)
```

This will output the same result as the previous method.

Advantages of `dict()` constructor:
- It is a more concise way of creating a copy compared to the `copy()` method.
- It also creates a shallow copy, preserving the same advantages and drawbacks as mentioned before.

### Method 3: Using the copy module

In addition to the built-in methods, Python also provides the `copy` module, which offers a more flexible approach to creating copies of objects, including dictionaries. The `copy` module allows you to create both shallow and deep copies of dictionaries.

```python
import copy

original_dict = {'a': 1, 'b': 2, 'c': {'x': 10, 'y': 20}}

# Create a shallow copy using copy module's copy() function
new_dict = copy.copy(original_dict)

# Modify the original dictionary
original_dict['a'] = 5
original_dict['c']['x'] = 100

# Print both dictionaries
print("Original Dictionary:", original_dict)
print("Shallow Copied Dictionary:", new_dict)
```

This will output:
```
Original Dictionary: {'a': 5, 'b': 2, 'c': {'x': 100, 'y': 20}}
Shallow Copied Dictionary: {'a': 1, 'b': 2, 'c': {'x': 100, 'y': 20}}
```

Advantages of `copy` module:
- It provides more control over the type of copy to be made.
- It allows for creating a deep copy of the dictionary, meaning all nested objects will also be copied recursively.

In conclusion, Python offers multiple ways to copy dictionaries, each suited for different scenarios. Depending on whether you need a shallow or deep copy, you can choose the appropriate method to ensure data integrity and prevent unintended modifications.