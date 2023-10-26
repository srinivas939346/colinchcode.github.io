---
layout: post
title: "[python] Syntax differences between dynamic typing and static typing in Python"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Python is a dynamically-typed language, meaning that variable types are determined at runtime. However, it does support type hints, which allow programmers to add static typing to their code.

## Dynamic Typing

In dynamic typing, variable types can change during runtime. This means that you don't need to explicitly declare the type of a variable before using it. Here's an example:

```python
x = 5
print(type(x))  # Output: <class 'int'>

x = "Hello"
print(type(x))  # Output: <class 'str'>
```

In the above code, the variable `x` is initially assigned an integer value, and its type is `int`. Later, the same variable is assigned a string value, and its type changes to `str`. This demonstrates the flexibility of dynamic typing.

## Static Typing (Type Hints)

Python also allows the use of static typing through the use of type hints, which are annotations added to function signatures and variable declarations. Static typing gives you better tooling support, improved code readability, and can help catch type-related errors early.

To use static typing in Python, you need to import the `annotations` module from the `typing` library and use the `: <type>` syntax to indicate the expected type. Here's an example:

```python
from typing import List

def sum_numbers(numbers: List[int]) -> int:
    total = 0
    for num in numbers:
        total += num
    return total
```

In the above code, the `sum_numbers` function expects a list of integers as input and returns an integer. By using type hints, we provide information about the expected types of the parameters and return value.

## Checking Types

Although Python itself doesn't enforce type checking, there are tools available that can check the types defined in type hints. One such tool is the **mypy** static type checker. With **mypy**, you can catch type errors before runtime by analyzing your type hints. Here's an example of running **mypy** on the previous code snippet:

```
$ mypy my_script.py
```

By running **mypy**, you can uncover and fix potential type-related issues even before executing the code.

## Conclusion

Dynamic typing in Python allows for flexibility and quick prototyping, while static typing through the use of type hints can provide better tooling support and improved code maintainability. By understanding the syntax differences between dynamic typing and static typing, you can choose the most suitable approach for your Python projects.

**References:**
- [Python Type Hints](https://docs.python.org/3/library/typing.html)
- [Mypy - Static Type Checking](http://mypy-lang.org/)