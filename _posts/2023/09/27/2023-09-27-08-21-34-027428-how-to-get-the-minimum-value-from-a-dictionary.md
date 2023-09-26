---
layout: post
title: "[python] How to get the minimum value from a dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

Dictionaries in Python are key-value pairs, where each value is associated with a unique key. Sometimes, you may want to find the minimum value from a dictionary based on the values it holds. In this blog post, we will explore different approaches to accomplish this task efficiently using Python.

## Method 1: Using the `min()` function

Python provides a built-in `min()` function that can be used to find the minimum value from any iterable, including dictionaries. We can use this function along with the `.values()` method of the dictionary to get the minimum value.

```python
my_dict = {'a': 10, 'b': 5, 'c': 20, 'd': 15}

min_value = min(my_dict.values())

print(f"The minimum value in the dictionary is: {min_value}")
```

Output:
```
The minimum value in the dictionary is: 5
```

In the above code, we first create a dictionary `my_dict` with a few key-value pairs. We then use the `min()` function to find the minimum value from the dictionary's values. Finally, we print the minimum value using a formatted string.

## Method 2: Using a loop

Another approach to find the minimum value from a dictionary is by iterating over its values using a loop.

```python
my_dict = {'a': 10, 'b': 5, 'c': 20, 'd': 15}

min_value = float('inf')  # set initial minimum value to positive infinity

for value in my_dict.values():
    if value < min_value:
        min_value = value

print(f"The minimum value in the dictionary is: {min_value}")
```

Output:
```
The minimum value in the dictionary is: 5
```

In this code, we initialize the `min_value` variable to a very large value using `float('inf')`. Then, we iterate over the dictionary's values and update the `min_value` variable if a smaller value is found.

## Method 3: Using a lambda function

We can also use a lambda function along with the `min()` function to find the minimum value from a dictionary.

```python
my_dict = {'a': 10, 'b': 5, 'c': 20, 'd': 15}

min_value = min(my_dict.values(), key=lambda x: x)

print(f"The minimum value in the dictionary is: {min_value}")
```

Output:
```
The minimum value in the dictionary is: 5
```

In this approach, we use a lambda function as the `key` argument to `min()`. The lambda function takes each value from the dictionary and returns it as is. This ensures that the minimum value is selected based on the original values.

## Conclusion

These are the three different methods to get the minimum value from a dictionary in Python. Depending on your use case, you can choose the most suitable approach. Remember to select the method that works best for the size of your dictionary and the performance requirements of your program.