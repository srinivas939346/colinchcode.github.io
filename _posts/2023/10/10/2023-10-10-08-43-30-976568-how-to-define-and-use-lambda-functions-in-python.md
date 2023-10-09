---
layout: post
title: "[python] How to define and use lambda functions in Python"
description: " "
date: 2023-10-10
tags: [python]
comments: true
share: true
---

In Python, **lambda functions** (also known as **anonymous functions**) are a way to create small, one-line functions without a **function name**. They are defined using the `lambda` keyword, followed by the function arguments and a colon `:` to separate the arguments from the function body. 

Lambda functions can be used wherever a function object is required. They are commonly used in scenarios where you need a simple and short function definition. 

## Syntax
The syntax for defining a lambda function is as follows:

```python
lambda arguments: expression
```

- `lambda`: The `lambda` keyword signals the creation of a lambda function.
- `arguments`: The arguments are the input parameters of the function.
- `expression`: The expression is the return value of the function.

## Example

Here is an example of a lambda function that takes two arguments and returns their sum:

```python
add = lambda x, y: x + y
print(add(5, 8))  # Output: 13
```

In this example, we define a lambda function `add` that takes two arguments `x` and `y` and returns their sum using the `+` operator. We then call the lambda function using the arguments `5` and `8`, and print the result.

## Using Lambda Functions

Lambda functions are often used in conjunction with higher-order functions like `map()`, `filter()`, and `reduce()` to perform operations on iterable objects.

Here are some examples of using lambda functions with built-in Python functions:

### 1. `map()`

The `map()` function applies a given function to each item in an iterable and returns a new iterable containing the results.

```python
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x ** 2, numbers))
print(squared)  # Output: [1, 4, 9, 16, 25]
```

In this example, we use a lambda function to square each item in the `numbers` list using the `map()` function. The resulting squared values are stored in the `squared` list.

### 2. `filter()`

The `filter()` function creates a new iterable containing the items from the original iterable for which the given function returns `True`.

```python
numbers = [1, 2, 3, 4, 5]
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
print(even_numbers)  # Output: [2, 4]
```

In this example, we use a lambda function to filter out the even numbers from the `numbers` list using the `filter()` function. The resulting even numbers are stored in the `even_numbers` list.

### 3. `reduce()`

The `reduce()` function applies a given function to the first two items in an iterable, then to the result and the next item, and so on, until a single value is obtained.

```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]
sum_of_numbers = reduce(lambda x, y: x + y, numbers)
print(sum_of_numbers)  # Output: 15
```

In this example, we use a lambda function to calculate the sum of all the numbers in the `numbers` list using the `reduce()` function.

## Conclusion

Lambda functions in Python provide a concise way to define small and simple functions. They are often used in combination with higher-order functions for efficient and elegant code. By understanding the syntax and usage of lambda functions, you can leverage their power to write more expressive and functional Python code.