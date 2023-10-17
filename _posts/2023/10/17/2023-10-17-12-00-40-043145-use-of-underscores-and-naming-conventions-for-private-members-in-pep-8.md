---
layout: post
title: "[python] Use of underscores and naming conventions for private members in PEP 8"
description: " "
date: 2023-10-17
tags: [python]
comments: true
share: true
---

When writing code in Python, it is important to follow the guidelines set out in PEP 8, the official style guide for Python code. One aspect of PEP 8 is the use of underscores and naming conventions for private members in Python classes.

## Undertanding the concept of private members

In Python, private members are variables and methods that are intended to be used only within the class they are defined in. They are not meant to be accessed or modified directly from outside the class. Python doesn't have a strict access control mechanism like some other languages, but developers conventionally use the concept of private members to convey their intended usage.

## Single Leading Underscore

According to PEP 8, a single leading underscore `_` should be used to indicate a weak "internal use" indicator. This convention suggests that the member is intended for internal use within the class or by subclasses, but it can still be accessed and modified by external code if needed. It serves as a gentle reminder to other developers that the member is not meant to be used outside the class unless necessary.

Here's an example that demonstrates the use of a single leading underscore for a private member variable:

```python
class MyClass:
    def __init__(self):
        self._private_variable = 10

    def _private_method(self):
        print("This is a private method.")

    def public_method(self):
        self._private_method()
        print("This is a public method.")
```

In the above example, `_private_variable` and `_private_method` are private members, indicated by the leading underscore. However, they can still be accessed and modified from outside the class if necessary.

## Double Leading Underscore

According to PEP 8, a double leading underscore `__` should be used to indicate a strong "internal use" indicator. This convention suggests that the member is intended to be used only within the class and its subclasses. Python performs name mangling on the member name, which makes it more difficult to access and modify directly from outside the class.

Here's an example that demonstrates the use of a double leading underscore for a private member variable:

```python
class MyClass:
    def __init__(self):
        self.__private_variable = 10

    def __private_method(self):
        print("This is a private method.")

    def public_method(self):
        self.__private_method()
        print("This is a public method.")
```

In the above example, `__private_variable` and `__private_method` are private members intended to be used only within the class. They are name-mangled to `_MyClass__private_variable` and `_MyClass__private_method`, respectively, making them more difficult to access from outside the class.

## Conclusion

Following the conventions suggested by PEP 8 for the use of underscores and naming conventions for private members in Python classes is a good practice. It improves code readability, makes the intent behind the members clear, and helps maintain a consistent coding style across projects.