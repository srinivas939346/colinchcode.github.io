---
layout: post
title: "[python] How to clear all items from a dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

In Python, you can clear all the items from a dictionary by using the `clear()` method. The `clear()` method removes all key-value pairs from the dictionary, making it empty.

Here's an example code snippet that demonstrates how to use the `clear()` method to clear all items from a dictionary:

```python
# Create a dictionary
my_dict = {'apple': 3, 'banana': 2, 'orange': 1}

# Display the original dictionary
print("Original dictionary:", my_dict)

# Clear all items from the dictionary
my_dict.clear()

# Display the updated dictionary
print("Updated dictionary:", my_dict)
```

Output:
```
Original dictionary: {'apple': 3, 'banana': 2, 'orange': 1}
Updated dictionary: {}
```

As you can see from the example, the `clear()` method removes all the items from the dictionary and leaves it empty.

It's important to note that calling the `clear()` method modifies the original dictionary directly. If you assign the dictionary to another variable before clearing it, both variables will reference the same empty dictionary afterward.

By using the `clear()` method, you can easily remove all items from a dictionary in Python.