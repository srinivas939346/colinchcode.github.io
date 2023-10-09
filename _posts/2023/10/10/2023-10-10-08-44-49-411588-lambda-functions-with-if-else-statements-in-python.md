---
layout: post
title: "[python] Lambda functions with if-else statements in Python"
description: " "
date: 2023-10-10
tags: [python]
comments: true
share: true
---

In Python, lambda functions are anonymous functions that can be declared inline. They are commonly used when a simple function is required for a short period of time.

Lambda functions can also include if-else statements to perform conditional operations. This allows for more complex functionality within a single lambda function.

In this blog post, we will explore how to use lambda functions with if-else statements in Python, and provide some examples to demonstrate their usage.

## Syntax of a Lambda Function with if-else

The general syntax of a lambda function with if-else statements is as follows:

```python
lambda arguments: expression_if_true if condition else expression_if_false
```

Here, `arguments` represent the input parameters of the lambda function. `expression_if_true` is the value returned if the condition is `True`, and `expression_if_false` is the value returned if the condition is `False`.

## Examples

Let's look at some examples to better understand how lambda functions with if-else statements work in Python.

### Example 1: Check if a number is even or odd

```python
is_even = lambda num: "even" if num % 2 == 0 else "odd"

print(is_even(4))  # Output: even
print(is_even(7))  # Output: odd
```

In this example, we define a lambda function `is_even` that takes an input `num`. If `num` is divisible by 2 (i.e., `num % 2 == 0`), it returns the string "even". Otherwise, it returns the string "odd".

### Example 2: Calculate the square or cube of a number

```python
calculate_result = lambda num, operation: num**2 if operation == "square" else num**3

print(calculate_result(2, "square"))  # Output: 4
print(calculate_result(3, "cube"))    # Output: 27
```

In this example, we create a lambda function `calculate_result` that takes two inputs `num` and `operation`. If `operation` is "square", it returns the square of `num` (`num**2`), and if `operation` is "cube", it returns the cube of `num` (`num**3`).

### Example 3: Filter even numbers from a list

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
even_numbers = list(filter(lambda num: num % 2 == 0, numbers))

print(even_numbers)  # Output: [2, 4, 6, 8, 10]
```

In this example, we use the `filter()` function along with a lambda function to filter even numbers from a list of `numbers`. The lambda function checks if each number in the list is even (`num % 2 == 0`) and returns `True` or `False` accordingly.

## Conclusion

Lambda functions with if-else statements provide a concise way to define conditional operations in Python. They are particularly useful when a small function is required for a specific task without the need for a named function. By using lambda functions with if-else statements, you can write more expressive and compact code.

Remember to consider the readability and maintainability of your code when deciding to use lambda functions with if-else statements, as overly complex expressions may make the code harder to understand.