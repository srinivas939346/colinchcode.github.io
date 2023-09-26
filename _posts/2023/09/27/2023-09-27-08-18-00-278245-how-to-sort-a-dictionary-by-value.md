---
layout: post
title: "[python] How to sort a dictionary by value?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

In Python, dictionaries are unordered collections of key-value pairs. However, if you want to sort a dictionary based on its values, you can achieve this by using the `sorted()` function along with a custom key argument.

Here's how you can sort a dictionary by its values:

```python
# Define a dictionary
my_dict = {'apple': 10, 'banana': 5, 'orange': 8, 'grape': 3}

# Sort the dictionary by value in ascending order
sorted_dict = dict(sorted(my_dict.items(), key=lambda x: x[1]))

# Print the sorted dictionary
print(sorted_dict)
```

In the code above, we have a dictionary called `my_dict`, with keys representing fruits and values representing their quantities. 

To sort the dictionary by value, we use the `sorted()` function on `my_dict.items()`, where `my_dict.items()` returns a list of key-value pairs. We pass a lambda function as the `key` argument to `sorted()`, which extracts the second element (the value) of each pair (`x[1]`).

Finally, we convert the sorted list of key-value pairs back into a dictionary using the `dict()` function, and store it in the `sorted_dict` variable.

When running the code, you will see that the dictionary is sorted in ascending order based on its values:

```
{'grape': 3, 'banana': 5, 'orange': 8, 'apple': 10}
```

You can also sort the dictionary in descending order by simply adding the `reverse=True` argument inside the `sorted()` function:

```python
sorted_dict = dict(sorted(my_dict.items(), key=lambda x: x[1], reverse=True))
```

Now the dictionary will be sorted in descending order based on the values:

```
{'apple': 10, 'orange': 8, 'banana': 5, 'grape': 3}
```

By sorting a dictionary based on its values, you can easily retrieve the keys in a specific order and perform various operations depending on your requirements.