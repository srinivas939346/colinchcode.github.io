---
layout: post
title: "[python] Lambda functions with nested if-else statements in Python"
description: " "
date: 2023-10-10
tags: [python]
comments: true
share: true
---

In Python, lambda functions are anonymous functions that can be defined using the `lambda` keyword. They are useful when a small function is needed for a particular task and don't require a formal function definition.

Lambda functions can handle nested if-else statements to perform conditional operations. This allows for more complex logic within the lambda function.

Here's an example of a lambda function with a nested if-else statement:

```python
add_numbers = lambda x, y: x + y if x > 0 else x - y

print(add_numbers(2, 3)) # Output: 5
print(add_numbers(-2, 3)) # Output: -5
```

In this example, the lambda function `add_numbers` takes two parameters `x` and `y`. If `x` is greater than 0, it returns the sum of `x` and `y`. Otherwise, it returns the difference between `x` and `y`.

To use the lambda function, simply call it with the required arguments. In this case, `add_numbers(2, 3)` returns 5 and `add_numbers(-2, 3)` returns -5.

Nested if-else statements can be further expanded to handle more complex conditions. Here's an example that checks multiple conditions:

```python
check_grade = lambda score: "A" if score >= 90 else "B" if score >= 80 else "C" if score >= 70 else "D" if score >= 60 else "F"

print(check_grade(95)) # Output: "A"
print(check_grade(85)) # Output: "B"
print(check_grade(75)) # Output: "C"
print(check_grade(65)) # Output: "D"
print(check_grade(55)) # Output: "F"
```

In this example, the lambda function `check_grade` takes a `score` parameter and returns a letter grade based on the score. The conditionals check for different score ranges and assign the respective grades.

Using nested if-else statements in lambda functions allows for compact and concise code. However, it's essential to keep the code readable and understandable to avoid confusion.