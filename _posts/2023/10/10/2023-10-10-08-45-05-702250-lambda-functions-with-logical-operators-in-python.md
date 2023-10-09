---
layout: post
title: "[python] Lambda functions with logical operators in Python"
description: " "
date: 2023-10-10
tags: [python]
comments: true
share: true
---

In Python, lambda functions are anonymous functions that can be defined in a single line of code. They are useful when you need a simple function without a name. Lambda functions are often used in combination with logical operators to perform conditional operations.

```python
# Example 1: Using logical operators in a lambda function
check_even = lambda x: x % 2 == 0
print(check_even(4))  # Output: True
print(check_even(7))  # Output: False
```

In the above example, we define a lambda function `check_even` that checks if a given number is even. It uses the modulo operator `%` to check if the number is divisible by 2, and the equality operator `==` to compare the result with 0. The lambda function returns `True` if the number is even, and `False` otherwise.

```python
# Example 2: Using logical operators in a lambda function
check_age = lambda age: age >= 18 and age <= 65
print(check_age(25))  # Output: True
print(check_age(12))  # Output: False
```

In this example, we define a lambda function `check_age` that checks if a given age is within the range of 18 to 65 (inclusive). The function uses the logical operators `and` to combine two conditions: `age >= 18` and `age <= 65`. If both conditions are true, the lambda function returns `True`; otherwise, it returns `False`.

Lambda functions with logical operators are useful in scenarios where you need to perform simple conditional checks without defining a separate named function. They can be used in various situations, such as filtering data, mapping values, or defining custom sorting functions.

Remember that lambda functions are typically used for simple and concise operations. For more complex scenarios, it's often better to define a named function using the `def` keyword instead.

I hope this article helped you understand how to use logical operators in lambda functions in Python. Experiment with different examples to get a better grasp of their usage in your own code.