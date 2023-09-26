---
layout: post
title: "[python] How to convert a nested dictionary into a flat dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

```python
def flatten_dictionary(d, parent_key='', sep='.'):
    flat_dict = {}
    for key, value in d.items():
        new_key = f"{parent_key}{sep}{key}" if parent_key else key

        if isinstance(value, dict):
            flat_dict.update(flatten_dictionary(value, new_key, sep=sep))
        else:
            flat_dict[new_key] = value

    return flat_dict
```

Here's how you can use the `flatten_dictionary` function:

```python
nested_dict = {
    'a': 1,
    'b': {
        'c': 2,
        'd': {
            'e': 3
        }
    }
}

flat_dict = flatten_dictionary(nested_dict)

print(flat_dict)
```

This will output:

```python
{
    'a': 1,
    'b.c': 2,
    'b.d.e': 3
}
```

In the resulting flat dictionary, the keys correspond to the full path of the values in the original nested dictionary.

By using recursion, this approach works for dictionaries with any level of nesting.