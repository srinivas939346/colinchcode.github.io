---
layout: post
title: "[python] Definition of static typing"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Python, being a dynamically-typed language by default, allows variables to be assigned any type of value without explicitly specifying its type. However, this flexibility can sometimes lead to errors that are only discovered at runtime.

Static typing addresses these issues by requiring developers to annotate their code with type hints, indicating the expected types of variables, function arguments, and return values. This information is used by static type checkers such as Mypy or Pyright to analyze the code and catch type-related errors before the program is executed.

To declare a static type in Python, you can use the `typing` module. For example:

```python
from typing import List, Dict

def calculate_average(numbers: List[int]) -> float:
    total = sum(numbers)
    average = total / len(numbers)
    return average

grades = [85, 92, 78, 90]
average_grade = calculate_average(grades)
```
In this example, the function `calculate_average` takes a list of integers (`List[int]`) as its argument and returns a float value (`float`). The type hints provide additional information about the expected types, allowing type checkers to detect potential issues like passing a non-integer value or assigning the returned value to a variable of the wrong type.

Static typing can improve code readability, maintainability, and catch errors early in the development process. However, it is important to note that Python's static typing is optional and the interpreter will not enforce it at runtime. It is primarily a tool to enhance developer productivity and code quality.

References:
- Python Typing: https://docs.python.org/3/library/typing.html
- Mypy: http://mypy-lang.org/
- Pyright: https://github.com/microsoft/pyright