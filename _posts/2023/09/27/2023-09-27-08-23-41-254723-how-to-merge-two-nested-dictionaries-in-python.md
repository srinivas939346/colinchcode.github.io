---
layout: post
title: "[python] How to merge two nested dictionaries in Python?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

In Python, merging two nested dictionaries can be achieved using the `update()` method. The `update()` method allows you to merge one dictionary into another. 

Here's an example:

```python
# Define two nested dictionaries
dict1 = {
    'outer_key1': {
        'inner_key1': 'value1',
        'inner_key2': 'value2'
    },
    'outer_key2': {
        'inner_key3': 'value3',
        'inner_key4': 'value4'
    }
}

dict2 = {
    'outer_key2': {
        'inner_key4': 'updated_value',
        'inner_key5': 'value5'
    },
    'outer_key3': {
        'inner_key6': 'value6',
        'inner_key7': 'value7'
    }
}

# Merge the nested dictionaries
dict1.update(dict2)

# Print the merged dictionary
print(dict1)
```

Output:

```python
{
    'outer_key1': {
        'inner_key1': 'value1',
        'inner_key2': 'value2'
    },
    'outer_key2': {
        'inner_key4': 'updated_value',
        'inner_key5': 'value5'
    },
    'outer_key3': {
        'inner_key6': 'value6',
        'inner_key7': 'value7'
    }
}
```

As you can see, the `update()` method merges the keys and values of `dict2` into `dict1`. If a key already exists in `dict1`, the value for that key will be updated with the value from `dict2`. If a key does not exist in `dict1`, it will be added with its corresponding value.

This method recursively merges nested dictionaries, ensuring that the sub-dictionaries are also merged correctly.

By using the `update()` method, you can easily merge two nested dictionaries in Python.