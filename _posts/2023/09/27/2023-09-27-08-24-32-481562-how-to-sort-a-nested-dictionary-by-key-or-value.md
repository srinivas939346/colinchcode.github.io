---
layout: post
title: "[python] How to sort a nested dictionary by key or value?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

## Sorting by Key

To sort a nested dictionary by key, we will use the `sorted()` function with a custom key function. Here's an example:

```python
nested_dict = {
    'b': {'age': 30},
    'c': {'age': 25},
    'a': {'age': 35}
}

sorted_dict = dict(sorted(nested_dict.items(), key=lambda x: x[0]))

print(sorted_dict)
```

The output will be:

```
{'a': {'age': 35}, 'b': {'age': 30}, 'c': {'age': 25}}
```

In this example, we use the `sorted()` function to sort the items of the nested dictionary based on their keys. The custom key function `lambda x: x[0]` ensures that the sorting is done based on the keys.

## Sorting by Value

To sort a nested dictionary by value, we need to access the values within each nested dictionary. Here's an example of how to accomplish this:

```python
nested_dict = {
    'b': {'age': 30},
    'c': {'age': 25},
    'a': {'age': 35}
}

sorted_dict = dict(sorted(nested_dict.items(), key=lambda x: x[1]['age']))

print(sorted_dict)
```

The output will be:

```
{'c': {'age': 25}, 'b': {'age': 30}, 'a': {'age': 35}}
```

In this example, we modify the key function to `lambda x: x[1]['age']`, which accesses the 'age' key within the nested dictionary and sorts accordingly.

## Conclusion

Sorting a nested dictionary in Python is achievable by leveraging the `sorted()` function and custom key functions. Whether sorting by key or value, these techniques will help you organize your data effectively. Remember to adapt the code to your specific use case and apply the appropriate modifications if necessary.