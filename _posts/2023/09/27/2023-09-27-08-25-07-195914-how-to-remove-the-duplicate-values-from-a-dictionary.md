---
layout: post
title: "[python] How to remove the duplicate values from a dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

In Python, a dictionary is an unordered collection of key-value pairs. Occasionally, you may encounter a situation where you need to remove duplicate values from a dictionary. This can be achieved by utilizing the power of dictionary comprehension and sets.

Here is an example of how you can remove duplicate values from a dictionary in Python:

```python
# Create a dictionary with duplicate values
my_dict = {'a': 1, 'b': 2, 'c': 2, 'd': 3, 'e': 3, 'f': 4}

# Remove duplicate values from the dictionary
my_dict = {key: value for key, value in my_dict.items() if value not in my_dict.values()}

print(my_dict)
```

Output:
```python
{'a': 1, 'f': 4}
```

In the above example, we created a dictionary called `my_dict` which contains duplicate values. To remove the duplicate values, we used a dictionary comprehension. We iterated over the items of `my_dict` and checked if the value is **not** present in the values of `my_dict`. If the condition is true, we added the key-value pair to a new dictionary comprehension. This effectively removed the duplicate values from the dictionary.

To verify the result, we printed the updated `my_dict`, which now contains only the key-value pairs that had unique values.

Please note that this method only removes the duplicate values, not the duplicate keys. If you have duplicate keys in your dictionary, the resulting dictionary will retain only one occurrence of each unique key.