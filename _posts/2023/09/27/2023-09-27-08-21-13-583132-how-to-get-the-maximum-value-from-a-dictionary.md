---
layout: post
title: "[python] How to get the maximum value from a dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

## Method 1: Using the `max()` function with the `values()` method

The first method involves using the built-in `max()` function along with the `values()` method of the dictionary. Here's an example:

```python
my_dict = {"apple": 10, "banana": 20, "orange": 15}

max_value = max(my_dict.values())
print("Maximum value:", max_value)
```

In this example, we have a dictionary `my_dict` with keys representing fruits and values representing their quantities. By calling the `values()` method on `my_dict`, we get a list-like view object containing all the values. We then pass that object as an argument to the `max()` function, which returns the maximum value. Finally, we print the result.

## Method 2: Using a loop to iterate through the dictionary

An alternative method involves iterating through the dictionary and keeping track of the maximum value using a loop. Here's an example:

```python
my_dict = {"apple": 10, "banana": 20, "orange": 15}

max_value = float("-inf")  # Start with a very low initial value

for value in my_dict.values():
    if value > max_value:
        max_value = value

print("Maximum value:", max_value)
```

In this approach, we initialize `max_value` with a very low initial value (negative infinity in this case). We then iterate through the values of the dictionary using a for loop. If we find a value that is greater than the current `max_value`, we update `max_value` with that value. At the end of the loop, we will have the maximum value stored in `max_value`.

## Conclusion

Finding the maximum value from a dictionary in Python can be achieved through different approaches. You can either use the `max()` function with the `values()` method or use a loop to iterate through the values and keep track of the maximum value. Both methods are efficient and straightforward. Choose the one that best suits your needs and coding style.

By using these techniques, you can efficiently extract the maximum value from a dictionary and apply them to solve various real-world problems.