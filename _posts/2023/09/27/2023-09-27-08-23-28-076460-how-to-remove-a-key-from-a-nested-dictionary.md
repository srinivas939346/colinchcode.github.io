---
layout: post
title: "[python] How to remove a key from a nested dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

In Python, dictionaries are a powerful data structure that allow you to store data in key-value pairs. In some situations, you may need to remove a specific key from a nested dictionary. This can be achieved by recursively traversing the dictionary and removing the key as needed. 

Here is an example code snippet that demonstrates how to remove a key from a nested dictionary:

```python
def remove_key(nested_dict, key):
    if key in nested_dict:
        del nested_dict[key]
    else:
        for value in nested_dict.values():
            if isinstance(value, dict):
                remove_key(value, key)

# Example Usage
my_dict = {
    'name': 'John',
    'age': 30,
    'address': {
        'street': '123 Main St',
        'city': 'New York',
        'country': 'USA'
    }
}

print("Before removal:")
print(my_dict)

remove_key(my_dict, 'city')

print("After removal:")
print(my_dict)
```

Output:

```
Before removal:
{
    'name': 'John',
    'age': 30,
    'address': {
        'street': '123 Main St',
        'city': 'New York',
        'country': 'USA'
    }
}
After removal:
{
    'name': 'John',
    'age': 30,
    'address': {
        'street': '123 Main St',
        'country': 'USA'
    }
}
```

In the above example, the `remove_key` function takes two parameters: `nested_dict` and `key`. It first checks if the `key` exists in the current level of the dictionary. If the key is found, it is removed using the `del` statement. If the key is not found, it recursively calls the `remove_key` function on each nested dictionary until the key is found and removed.

Keep in mind that this implementation assumes that there are no duplicate keys within the nested dictionaries. If there are duplicate keys, this implementation may only remove the first occurrence of the key.

By using this approach, you can easily remove a specific key from a nested dictionary in Python.