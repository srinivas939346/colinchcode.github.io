---
layout: post
title: "[python] How to check if a value exists in a dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

In Python, you can check if a value exists in a dictionary by using the `in` keyword or the `.values()` method. 

The `in` keyword allows you to check if a value is present in the keys of the dictionary. Here's how you can use it:

```python
# Create a dictionary
my_dict = {'name': 'John', 'age': 25, 'city': 'New York'}

# Check if a value exists in the dictionary
if 'John' in my_dict.values():
    print('Value found!')
else:
    print('Value not found!')
```

In this example, the `.values()` method is used to get a view object of the dictionary's values. The `in` keyword checks if the value `'John'` is present in the view object.

Output:
```
Value found!
```

Alternatively, you can directly use the `.values()` method to check if a value exists in the dictionary:

```python
# Create a dictionary
my_dict = {1: 'one', 2: 'two', 3: 'three'}

# Check if a value exists in the dictionary
if 'two' in my_dict.values():
    print('Value found!')
else:
    print('Value not found!')
```

Output:
```
Value found!
```

These methods can be useful when you need to validate whether a specific value is present in a dictionary or not.