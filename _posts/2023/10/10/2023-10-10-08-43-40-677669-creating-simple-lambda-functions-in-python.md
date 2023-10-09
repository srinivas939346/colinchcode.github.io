---
layout: post
title: "[python] Creating simple lambda functions in Python"
description: " "
date: 2023-10-10
tags: [python]
comments: true
share: true
---

In Python, lambda functions, also known as anonymous functions, are compact and inline functions that can be created without using the `def` keyword. Lambda functions are often used in situations where a small function needs to be defined on the fly, without explicitly naming it.

### Syntax of a lambda function

The syntax of a lambda function in Python is as follows:

```python
lambda arguments: expression
```

Here, `arguments` are the input parameters for the function, and `expression` is the computation that the function will perform.

### Examples of using lambda functions

#### Example 1: Adding two numbers

```python
add = lambda x, y: x + y
print(add(2, 3))  # Output: 5
```

In this example, we are creating a lambda function called `add` that takes two arguments `x` and `y` and returns their sum.

#### Example 2: Checking if a number is even

```python
is_even = lambda n: n % 2 == 0
print(is_even(4))  # Output: True
print(is_even(7))  # Output: False
```

Here, we define a lambda function `is_even` that checks if a given number `n` is even or not. It returns `True` if the number is even, else `False`.

#### Example 3: Sorting a list of strings based on length

```python
fruits = ["apple", "banana", "cherry", "date"]
sorted_fruits = sorted(fruits, key=lambda s: len(s))
print(sorted_fruits)  # Output: ['date', 'apple', 'cherry', 'banana']
```

In this example, we use a lambda function as the `key` argument in the `sorted` function. The lambda function `lambda s: len(s)` computes the length of each string in the list `fruits` and sorts the list based on the string lengths.

### Benefits of using lambda functions

Lambda functions have a few advantages over regular functions:

1. **Compactness**: Lambda functions enable us to write concise and compact code. They are especially useful when we need to define a small function without cluttering the code.

2. **No need for naming**: Lambda functions do not require a function name. This makes them convenient in situations where we need a function for a one-time or temporary use.

3. **Inline usage**: Lambda functions can be used directly as arguments to other functions or as elements in functional programming constructs like `map`, `filter`, and `reduce`.

Lambda functions are a powerful feature in Python that allow for more expressive and concise code. They are widely used in functional programming paradigms and are valuable in scenarios where a small, anonymous function is needed.