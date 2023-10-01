---
layout: post
title: "[python] Boundary testing in Python"
description: " "
date: 2023-10-02
tags: [python]
comments: true
share: true
---

Boundary testing is a software testing technique where test cases are designed to evaluate the system's behavior at the boundaries of its input ranges. The purpose is to check if the system handles both valid and invalid inputs correctly and produces the expected output.

In this blog post, we will explore how to perform boundary testing in Python using various approaches.

## Table of Contents
- [What is Boundary Testing?](#what-is-boundary-testing)
- [Boundary Testing Techniques](#boundary-testing-techniques)
- [Examples of Boundary Testing in Python](#examples-of-boundary-testing-in-python)
    - [Boundary Testing for Integer Input](#boundary-testing-for-integer-input)
    - [Boundary Testing for String Length](#boundary-testing-for-string-length)
    - [Boundary Testing for List Index](#boundary-testing-for-list-index)
- [Conclusion](#conclusion)

## What is Boundary Testing?
Boundary testing involves testing the system with inputs that are at the upper and lower limits of the input range or just inside and outside of these limits. It helps identify any issues related to data validation, rounding errors, and handling extreme values.

Boundary testing is particularly useful when there are specific constraints or limits on the inputs the system can accept. By testing at the boundaries, you can ensure that the system handles edge cases correctly and does not produce unexpected results.

## Boundary Testing Techniques
Some common techniques used for boundary testing include:
- **Boundary Value Analysis**: This technique focuses on testing values at the boundaries of the input ranges, such as the minimum, maximum, and just inside/outside of these limits.
- **Equivalence Partitioning**: This technique divides the input range into smaller partitions and selects representative values from each partition for testing.
- **Worst-Case Testing**: This technique involves testing with inputs that lead to the worst possible outcome or performance of the system.

## Examples of Boundary Testing in Python

### Boundary Testing for Integer Input
Let's consider a simple function that checks if an input number `num` is within a specified range:

```python
def is_in_range(num, lower_limit, upper_limit):
    if num >= lower_limit and num <= upper_limit:
        return True
    else:
        return False

# Boundary testing for integer input
print(is_in_range(5, 0, 10))  # True
print(is_in_range(0, 0, 10))  # True
print(is_in_range(10, 0, 10))  # True
print(is_in_range(-1, 0, 10))  # False
print(is_in_range(11, 0, 10))  # False
```

In this example, we test the function with inputs that are at the lower boundary (`0`), upper boundary (`10`), and just inside/outside these boundaries.

### Boundary Testing for String Length
Consider a function that checks if the length of a string `text` is within a specified range:

```python
def is_valid_length(text, lower_limit, upper_limit):
    if len(text) >= lower_limit and len(text) <= upper_limit:
        return True
    else:
        return False

# Boundary testing for string length
print(is_valid_length("Hello", 2, 5))  # True
print(is_valid_length("", 2, 5))  # False
print(is_valid_length("Hello World", 2, 5))  # False
```

Here we test the function with strings of different lengths, including strings at the lower boundary (`2`), upper boundary (`5`), and just inside/outside these boundaries.

### Boundary Testing for List Index
Let's consider a function that retrieves an item at a specific index `index` from a given list `lst`:

```python
def get_item_at_index(lst, index):
    if index >= 0 and index < len(lst):
        return lst[index]
    else:
        return None

# Boundary testing for list index
my_list = [1, 2, 3, 4, 5]
print(get_item_at_index(my_list, 0))  # 1
print(get_item_at_index(my_list, 4))  # 5
print(get_item_at_index(my_list, -1))  # None
print(get_item_at_index(my_list, 5))  # None
```

In this example, we test the function with different indexes, including the lower boundary (`0`), upper boundary (`4`), and just inside/outside these boundaries.

## Conclusion
Boundary testing is an essential technique for ensuring the robustness of software systems. It helps to identify and handle edge cases effectively. In this blog post, we explored several examples of performing boundary testing in Python using different scenarios. By utilizing various techniques and testing at the boundaries, you can uncover potential issues and ensure the reliability of your code.