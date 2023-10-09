---
layout: post
title: "[python] Lambda functions with conditionals in Python"
description: " "
date: 2023-10-10
tags: [python]
comments: true
share: true
---

Lambda functions, also known as anonymous functions, are a concise way to define small, unnamed functions in Python. They can be particularly useful when you need to define a simple function on the fly without the need for a formal function definition.

In addition to their simplicity, lambda functions can also include conditionals, allowing you to create more complex logic within a single line of code.

## Syntax of lambda functions with conditionals

The syntax for a lambda function with conditionals is as follows:

```python
lambda <arguments>: <expression_if_true> if <condition> else <expression_if_false>
```

Let's break down the syntax components:
- `lambda`: the keyword used to define a lambda function.
- `<arguments>`: the comma-separated list of arguments that the lambda function takes.
- `<expression_if_true>`: the expression to be evaluated if the condition is true.
- `if <condition>`: the condition to be checked.
- `<expression_if_false>`: the expression to be evaluated if the condition is false.

## Examples of lambda functions with conditionals

Here are a few examples to illustrate the usage of lambda functions with conditionals:

### Example 1: Absolute value function

```python
absolute_value = lambda x: x if x >= 0 else -x
print(absolute_value(5))  # Output: 5
print(absolute_value(-3))  # Output: 3
```

In this example, the lambda function `absolute_value` returns the absolute value of a number. If the number is greater than or equal to zero, it returns the number itself. Otherwise, it returns the negative of the number.

### Example 2: Even or odd checker

```python
even_or_odd = lambda x: "Even" if x % 2 == 0 else "Odd"
print(even_or_odd(4))  # Output: Even
print(even_or_odd(7))  # Output: Odd
```

The lambda function `even_or_odd` checks whether a given number is even or odd. If the number is divisible by 2 (i.e., the remainder is 0), it returns "Even". Otherwise, it returns "Odd".

### Example 3: Grade evaluator

```python
grade_evaluator = lambda grade: "Pass" if grade >= 50 else "Fail"
print(grade_evaluator(80))  # Output: Pass
print(grade_evaluator(30))  # Output: Fail
```

In this example, the lambda function `grade_evaluator` evaluates a grade and returns "Pass" if the grade is greater than or equal to 50. Otherwise, it returns "Fail".

## Conclusion

Lambda functions with conditionals allow for more complex logic to be written in a concise and efficient manner. They are particularly useful for defining small and anonymous functions on the fly. However, it's important to use them judiciously to maintain code readability and understandability.