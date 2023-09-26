---
layout: post
title: "[python] How to find the intersection of two dictionaries?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

Python dictionaries are powerful data structures that store key-value pairs. At times, you may need to find the intersection - or the common elements - between two dictionaries. In this article, we will explore different methods to achieve this using Python.

## Method 1: Using Dictionary Comprehension

One approach to find the intersection of dictionaries is by using dictionary comprehension. Here's an example:

```python
def find_intersection(dict1, dict2):
    return {key: dict1[key] for key in dict1 if key in dict2 and dict1[key] == dict2[key]}
```

Let's break down the above code:
- `dict1[key] for key in dict1` iterates over all the keys in `dict1`.
- The `if` condition `key in dict2 and dict1[key] == dict2[key]` checks if the key is present in `dict2` and if the corresponding values match.
- The key-value pairs that satisfy the condition are added to the result dictionary using `key: dict1[key]`.

You can now call the `find_intersection` function with your dictionaries to find their common elements:

```python
dict1 = {'apple': 1, 'banana': 2, 'orange': 3}
dict2 = {'banana': 2, 'kiwi': 4, 'orange': 5}

result = find_intersection(dict1, dict2)
print(result)  # Output: {'banana': 2}
```

## Method 2: Using the `items()` Method

An alternative method is to use the `items()` method of dictionaries. This method returns a view object that contains the key-value pairs of the dictionary. Here's an example:

```python
def find_intersection(dict1, dict2):
    return {key: dict1[key] for key, value in dict1.items() if key in dict2 and value == dict2[key]}
```

The `for` loop `key, value in dict1.items()` in the above code iterates over each key-value pair in `dict1`, allowing us to compare keys and values simultaneously.

You can now call the `find_intersection` function:

```python
dict1 = {'apple': 1, 'banana': 2, 'orange': 3}
dict2 = {'banana': 2, 'kiwi': 4, 'orange': 5}

result = find_intersection(dict1, dict2)
print(result)  # Output: {'banana': 2}
```

## Conclusion

Finding the intersection of two dictionaries in Python is an essential operation when dealing with data manipulation. By using either dictionary comprehension or the `items()` method, you can easily extract the common elements between two dictionaries.