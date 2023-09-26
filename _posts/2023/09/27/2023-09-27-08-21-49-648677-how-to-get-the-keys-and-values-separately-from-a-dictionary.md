---
layout: post
title: "[python] How to get the keys and values separately from a dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---
title: "Getting Keys and Values from a Dictionary in Python"
date: "2021-09-01"
categories:
  - Python
tags:
  - dictionary
  - keys
  - values
---

One of the most powerful data structures in Python is the dictionary. It allows you to store and retrieve data using key-value pairs. Sometimes, you may need to extract the keys or values separately from a dictionary for further processing or analysis. In this tutorial, we will learn how to do that in Python.

To get the keys and values separately from a dictionary, you can use the `keys()` and `values()` methods available for dictionaries in Python. Let's see how this is done:

```python
# Sample dictionary
my_dict = {'name': 'John', 'age': 30, 'city': 'New York'}

# Get the keys
keys = my_dict.keys()
print("Keys:", keys)

# Get the values
values = my_dict.values()
print("Values:", values)
```

In the above code, we define a dictionary `my_dict` with some key-value pairs. To retrieve the keys, we use the `keys()` method on the dictionary, which returns a view object containing all the keys. Similarly, to get the values, we use the `values()` method, which returns a view object containing all the values.

We can iterate over these view objects to access the keys and values individually:

```python
# Iterate over keys
for key in keys:
    print("Key:", key)

# Iterate over values
for value in values:
    print("Value:", value)
```

Alternatively, if you need to convert the keys or values to a list, you can use the `list()` function:

```python
# Convert keys to list
key_list = list(keys)

# Convert values to list
value_list = list(values)
```

By using the `keys()` and `values()` methods, you can extract the keys and values separately from a dictionary in Python. This can be helpful when you need to perform operations on only the keys or values in your code.

Remember to handle exceptions if you try to access a non-existing key or value from the dictionary to avoid errors.