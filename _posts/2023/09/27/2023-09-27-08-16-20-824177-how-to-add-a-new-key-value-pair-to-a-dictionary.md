---
layout: post
title: "[python] How to add a new key-value pair to a dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---
title: Python - Adding a New Key-Value Pair to a Dictionary
seo_title: Python Dictionary - Adding Key-Value Pair
description: Learn how to add a new key-value pair to a dictionary in Python.
---

In Python, a dictionary is a useful data structure to store key-value pairs. Adding a new key with its corresponding value to a dictionary can be easily done using the built-in methods provided by the language. In this article, you will learn different ways to add a new key-value pair to a dictionary in Python.

## Using Bracket Notation

One way to add a new key-value pair to a dictionary is by using the bracket notation. Here's an example:

```python
my_dict = {'name': 'John', 'age': 25}
my_dict['city'] = 'New York'
print(my_dict)
```

Output:
```
{'name': 'John', 'age': 25, 'city': 'New York'}
```

In the above code, we have a dictionary `my_dict` with two key-value pairs - `'name': 'John'` and `'age': 25`. We use the bracket notation to add a new key `'city'` with the value `'New York'`. After adding the new key-value pair, we print the updated dictionary.

## Using the `update()` Method

Another method to add a new key-value pair to a dictionary is by using the `update()` method. Here's an example:

```python
my_dict = {'name': 'John', 'age': 25}
my_dict.update({'city': 'New York'})
print(my_dict)
```

Output:
```
{'name': 'John', 'age': 25, 'city': 'New York'}
```

In this code snippet, we have a similar dictionary `my_dict`. Using the `update()` method, we pass a dictionary with the new key-value pair as an argument. The `update()` method merges the passed dictionary with the existing dictionary and adds any new key-value pairs.

## Conclusion

You can add a new key-value pair to a dictionary in Python using either the bracket notation or the `update()` method. Dictionaries are versatile data structures that allow efficient retrieval and modification of values based on their keys. Adding key-value pairs to dictionaries can be useful when working with data that requires mapping between unique keys and values.