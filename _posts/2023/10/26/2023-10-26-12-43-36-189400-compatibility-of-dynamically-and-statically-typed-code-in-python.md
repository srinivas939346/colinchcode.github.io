---
layout: post
title: "[python] Compatibility of dynamically and statically typed code in Python"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Python is a dynamically typed programming language, which means that variable types are determined at runtime. However, it is also possible to write statically typed code in Python using type hints introduced in Python 3.5. This allows developers to annotate variables and function arguments with their expected types.

## Dynamic Typing in Python

Dynamic typing in Python offers flexibility and simplicity. Developers can easily assign different types of values to the same variable without explicitly declaring its type. This can be advantageous in situations where the type may change during runtime or when writing code that needs to be more flexible.

For example, in a dynamically typed language like Python, we can assign an integer to a variable and later assign a string to the same variable without any issues:

```python
x = 10
print(x)  # Output: 10

x = "Hello, world!"
print(x)  # Output: Hello, world!
```

## Statically Typed Code with Type Hints

Starting from Python 3.5, static typing was introduced using type hints. Type hints allow developers to specify the expected types of variables and function arguments. Although these hints are not enforced at runtime, they provide a way to add clarity and improve code quality.

To use type hints, you can import the `typing` module and annotate your variables and function arguments with the desired types. Here's an example of static typing in Python:

```python
from typing import List

def sum_numbers(numbers: List[int]) -> int:
    return sum(numbers)

numbers_list = [1, 2, 3, 4, 5]
result = sum_numbers(numbers_list)
print(result)  # Output: 15
```

In the above code, the `numbers` parameter of the `sum_numbers` function is annotated with the type `List[int]`, indicating that it expects a list of integers as input.

## Compatibility between Dynamic and Static Code

Dynamically typed code can call statically typed code, and vice versa, without any issues. Python allows both dynamically and statically typed code to coexist and work together seamlessly.

When dynamically typed code calls a function that has static type hints, it is not mandatory to pass arguments of the exact expected type. Python will perform type inference and attempt to convert the argument to the expected type if possible. In case of any mismatches, a type checker tool like `mypy` can be used to spot potential issues during development.

Similarly, when statically typed code calls a function that does not have type hints or is dynamically typed, the type hints are simply ignored, and the function can be invoked as usual.

## Conclusion

Python's dynamic and static typing features offer flexibility and simplicity, as well as the ability to add type hints for improved code clarity. The compatibility between dynamically and statically typed code allows developers to choose the level of type checking that best suits their project, making Python suitable for various use cases.