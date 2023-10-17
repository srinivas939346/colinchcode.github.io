---
layout: post
title: "[python] Use of singletons and constant values in PEP 8"
description: " "
date: 2023-10-17
tags: [python]
comments: true
share: true
---

In Python, singletons and constant values are widely used to improve code readability and maintainability. The PEP 8 style guide provides recommendations on how to use them effectively. In this article, we will explore the best practices for using singletons and constant values in accordance with PEP 8.

## Singletons

A singleton is a design pattern that ensures only one instance of a class exists throughout the application. It can be useful when you want to have a single point of control for a particular resource or functionality.

### Naming Convention

According to PEP 8, the name of a singleton should be in `UPPER_CASE_WITH_UNDERSCORES` to indicate that it is intended to be a constant, and the value should be assigned using a class attribute.

Example:

```python
class SingletonClass:
    INSTANCE = None

    def __new__(cls, *args, **kwargs):
        if cls.INSTANCE is None:
            cls.INSTANCE = super().__new__(cls, *args, **kwargs)
        return cls.INSTANCE
```

### Usage

To use a singleton, you can simply instantiate the class, which will always return the same instance.

Example:

```python
obj1 = SingletonClass()
obj2 = SingletonClass()

print(obj1 is obj2)  # Output: True
```

## Constant Values

Constant values are used to represent fixed and unchanging values in our code. PEP 8 recommends using uppercase letters for constant names to distinguish them from regular variables.

### Naming Convention

A constant value should be named in `UPPER_CASE_WITH_UNDERSCORES` to indicate its immutability.

Example:

```python
MY_CONSTANT = 42
```

### Usage

Throughout your code, you can use the constant value directly by referring to its name.

Example:

```python
result = MY_CONSTANT * 2

print(result)  # Output: 84
```

## References

- [PEP 8 -- Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/)
- [Singleton Design Pattern in Python](https://refactoring.guru/design-patterns/singleton/python)
- [Python Constants and Naming Conventions](https://stackoverflow.com/questions/15981042/python-constants-and-naming-conventions)