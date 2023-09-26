---
layout: post
title: "[python] How to access keys in a dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

In Python, a dictionary is a collection of key-value pairs where each key is unique. To access the keys in a dictionary, you can use the built-in `keys()` method.

Here's an example:

```python
# Create a dictionary
my_dict = {'name': 'John', 'age': 30, 'city': 'New York'}

# Access keys using the keys() method
keys = my_dict.keys()

# Print the keys
for key in keys:
    print(key)
```

In the above code, we have a dictionary `my_dict` with keys `'name'`, `'age'`, and `'city'`. We use the `keys()` method to extract the keys and store them in the `keys` variable. Then, we iterate over the keys and print each key.

The output will be:

```
name
age
city
```

You can also convert the keys into a list using the `list()` function if you need to manipulate them further:

```python
# Convert keys to a list
key_list = list(my_dict.keys())

# Print the key list
print(key_list)
```

The output will be:

```
['name', 'age', 'city']
```

By accessing the keys in a dictionary, you can retrieve and work with specific key-value pairs or perform operations based on the keys in your code.