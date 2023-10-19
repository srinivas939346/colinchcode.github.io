---
layout: post
title: "[python] Encapsulation in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

In object-oriented programming, encapsulation refers to the binding of data and methods within a single unit called a class. It allows the data to be hidden from external access and provides a way to control how the data can be modified or accessed by other parts of the program. In Python, encapsulation is achieved using access modifiers and getter/setter methods.

## Access Modifiers

Python provides three access modifiers that can be used to control the visibility of variables and methods within a class:

- **Public**: Variables and methods that are not prefixed with an underscore (_) are considered public and can be accessed from anywhere, even outside the class.

- **Protected**: Variables and methods that are prefixed with a single underscore (_) are considered protected and can only be accessed from within the class and its subclasses.

- **Private**: Variables and methods that are prefixed with double underscores (__) are considered private and can only be accessed from within the class itself.

```python
class MyClass:
    def __init__(self):
        self.public_var = "Public"
        self._protected_var = "Protected"
        self.__private_var = "Private"
        
    def public_method(self):
        print("This is a public method")
        
    def _protected_method(self):
        print("This is a protected method")
        
    def __private_method(self):
        print("This is a private method")
```

In the example above, `public_var`, `public_method`, `_protected_var`, `_protected_method`, `__private_var`, and `__private_method` are the respective public, protected, and private variables and methods of the `MyClass` class.

## Getter and Setter Methods

To access or modify private variables, getter and setter methods can be used. Getter methods are used to fetch the value of a private variable, while setter methods are used to set the value of a private variable.

```python
class MyClass:
    def __init__(self):
        self.__private_var = 0

    def get_private_var(self):
        return self.__private_var

    def set_private_var(self, value):
        self.__private_var = value
```

In the above example, the `get_private_var()` method returns the value of the private variable `__private_var`, and the `set_private_var(value)` method sets the value of `__private_var` to the provided `value`.

## Example Usage

```python
obj = MyClass()
print(obj.get_private_var())  # Output: 0

obj.set_private_var(10)
print(obj.get_private_var())  # Output: 10
```

In the example usage above, the `get_private_var()` method is used to fetch the value of `__private_var`, and the `set_private_var(value)` method is used to set a new value for `__private_var`.

Encapsulation is an essential concept in object-oriented programming as it promotes data security and provides a way to maintain the integrity of the class by controlling access to its internal state.