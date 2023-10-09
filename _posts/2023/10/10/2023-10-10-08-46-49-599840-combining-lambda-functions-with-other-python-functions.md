---
layout: post
title: "[python] Combining lambda functions with other Python functions"
description: " "
date: 2023-10-10
tags: [python]
comments: true
share: true
---

Lambda functions, also known as anonymous functions, are a powerful feature of Python. They allow you to create small, one-line functions without using the `def` keyword. Although lambda functions are limited to just a single expression, they can be combined with other Python functions to perform complex operations efficiently. In this article, we will explore how to combine lambda functions with other Python functions effectively.

## Table of Contents
1. [Combining Lambda Functions with `map()`](#combining-lambda-functions-with-map)
2. [Combining Lambda Functions with `filter()`](#combining-lambda-functions-with-filter)
3. [Combining Lambda Functions with `reduce()`](#combining-lambda-functions-with-reduce)
4. [Combining Lambda Functions with Custom Functions](#combining-lambda-functions-with-custom-functions)
5. [Conclusion](#conclusion)

## Combining Lambda Functions with `map()`
The `map()` function in Python applies a given function to each item in an iterable and returns a new iterator. Lambda functions work seamlessly with `map()` to apply a specific operation on every element of an iterable.

```python
nums = [1, 2, 3, 4, 5]
doubled_nums = list(map(lambda x: x * 2, nums))
print(doubled_nums)  # Output: [2, 4, 6, 8, 10]
```

In the example above, we use a lambda function to double each number in the `nums` list using `map()`. The result is a new list, `doubled_nums`, with each element doubled.

## Combining Lambda Functions with `filter()`
The `filter()` function in Python takes an iterable and filters out the items based on a given function that returns boolean values. Lambda functions can be used effectively with `filter()` to create a filtered list that meets specific criteria.

```python
nums = [1, 2, 3, 4, 5]
even_nums = list(filter(lambda x: x % 2 == 0, nums))
print(even_nums)  # Output: [2, 4]
```

In the example above, the lambda function checks whether a number is divisible by 2. The `filter()` function then uses this lambda function to filter out all the odd numbers from the `nums` list, resulting in a new list, `even_nums`, that contains only the even numbers.

## Combining Lambda Functions with `reduce()`
The `reduce()` function in Python applies a rolling computation to a sequence of elements and returns a single accumulated value. Although `reduce()` is not a built-in function in Python 3, it can be imported from the `functools` module. Lambda functions can be combined with `reduce()` to perform operations like summing all the elements in a list.

```python
from functools import reduce

nums = [1, 2, 3, 4, 5]
sum = reduce(lambda x, y: x + y, nums)
print(sum)  # Output: 15
```

In the above example, we use a lambda function with two arguments, `x` and `y`, to calculate the sum of all the numbers in the `nums` list using `reduce()`. The result is stored in the `sum` variable.

## Combining Lambda Functions with Custom Functions
Lambda functions can also be combined with custom functions to perform more complex operations. It allows you to create concise and readable code by defining inline functions without the need for a separate function definition.

```python
def multiply_by_two(x):
    return x * 2

nums = [1, 2, 3, 4, 5]
modified_nums = list(map(lambda x: multiply_by_two(x), nums))
print(modified_nums)  # Output: [2, 4, 6, 8, 10]
```

In the example above, we have a custom function `multiply_by_two()`, which multiplies a number by two. We combine this custom function with a lambda function and `map()` to apply the `multiply_by_two()` function to each element of the `nums` list.

## Conclusion
By combining lambda functions with other Python functions like `map()`, `filter()`, `reduce()`, or custom functions, you can perform powerful operations on iterables in a concise and efficient manner. Lambda functions add flexibility and expressiveness to your code, allowing you to handle complex tasks with ease.