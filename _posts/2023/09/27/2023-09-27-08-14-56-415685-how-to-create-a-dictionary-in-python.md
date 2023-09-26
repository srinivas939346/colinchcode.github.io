---
layout: post
title: "[python] How to create a dictionary in Python?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

A dictionary in Python is a **collection of key-value pairs**. It is also known as a hash table or associative array. Dictionaries are one of the most versatile and commonly used data structures in Python.

To create a dictionary in Python, you can follow these steps:

1. **Using curly braces {}**
    
    ```python
    my_dict = {}
    ```
    
    By creating an empty dictionary using curly braces, you can add key-value pairs later.
    

2. **Using the dict() constructor**

    ```python
    my_dict = dict()
    ```
    
    The `dict()` constructor creates an empty dictionary.
    

3. **Initializing with key-value pairs**

    ```python
    my_dict = {"key1": "value1", "key2": "value2", "key3": "value3"}
    ```
    
    You can initialize a dictionary by providing key-value pairs within curly braces. Each key-value pair is separated by a colon ':'.

Let's look at some examples to better understand how to create dictionaries:

```python
# Example 1: Creating an empty dictionary
my_dict = {}

# Example 2: Using the dict() constructor
my_dict = dict()

# Example 3: Initializing a dictionary with key-value pairs
my_dict = {"name": "John", "age": 30, "city": "New York"}

# Example 4: Adding key-value pairs later
my_dict["occupation"] = "Software Engineer"
my_dict["company"] = "ABC Inc."

print(my_dict)
```

Output:
```
{'name': 'John', 'age': 30, 'city': 'New York', 'occupation': 'Software Engineer', 'company': 'ABC Inc.'}
```

In the last example, we added two new key-value pairs using square brackets and assigned corresponding values.

Dictionaries are a powerful data structure in Python and can be used to store and manipulate a wide variety of data types. They provide a convenient way to access and retrieve values using their associated keys.

Now that you know how to create dictionaries in Python, you can start using them in your programs and take advantage of their flexibility and efficiency.