---
layout: post
title: "[python] Lambda functions with math operators in Python"
description: " "
date: 2023-10-10
tags: [python]
comments: true
share: true
---

In Python, lambda functions provide a concise way to create small anonymous functions. They offer a convenient syntax for defining functions on-the-fly without the need for a formal `def` statement. Lambda functions can be particularly useful when working with math operators.

Here's an example of using lambda functions with math operators in Python:

## Addition

```python
add = lambda x, y: x + y
result = add(5, 10)
print(result)  # Output: 15
```

In the example above, we define a lambda function `add` that takes two arguments `x` and `y` and returns their sum. We then invoke this lambda function by passing `5` and `10` as arguments, and store the result in the variable `result`. Finally, we print the result, which is `15`.

## Subtraction

```python
subtract = lambda x, y: x - y
result = subtract(10, 5)
print(result)  # Output: 5
```

In this example, we define a lambda function `subtract` that takes two arguments `x` and `y` and returns their difference. Similar to the addition example, we invoke the function with `10` and `5` as arguments, and store the result in `result`. Printing the value of `result` yields `5`.

## Multiplication

```python
multiply = lambda x, y: x * y
result = multiply(3, 4)
print(result)  # Output: 12
```

Here, we create a lambda function `multiply` that multiplies two numbers `x` and `y`. The lambda function is then called with arguments `3` and `4`, assigning the resulting value to `result`. The printed output is `12`.

## Division

```python
divide = lambda x, y: x / y
result = divide(10, 2)
print(result)  # Output: 5.0
```

In this example, we define a lambda function `divide` to perform division. The function takes two arguments `x` and `y`, divides `x` by `y`, and returns the result. The lambda function is invoked with `10` and `2` as arguments, and the result is stored in `result`. The printed output is `5.0`.

Lambda functions with math operators provide an elegant way to create small, one-time-use functions for performing common mathematical operations in Python. They are especially useful when writing short, concise code or when using functions as arguments in higher-order functions.

Remember, lambda functions are best suited for simple operations. For more complex tasks, it is often recommended to define regular functions using the `def` statement.