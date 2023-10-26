---
layout: post
title: "[python] Dynamic typing and duck typing in Python"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Python is known for its dynamic typing and duck typing features, which make it a versatile and flexible programming language. These features allow developers to write code that is more concise and expressive. In this blog post, we will explore the concepts of dynamic typing and duck typing in Python.

## Dynamic Typing
Python is a dynamically typed language, which means that the type of a variable is determined at runtime. Unlike statically typed languages where the type is determined at compile-time, in Python, the type of a variable can change throughout the execution of a program.

```python
# Dynamic Typing in Python
x = 5  # x is an integer
print(x)

x = "Hello, World!"  # x is now a string
print(x)
```

In the code snippet above, we assign an integer value to the variable `x` initially, and later assign a string value to the same variable. This demonstrates the dynamic typing nature of Python.

Dynamic typing in Python provides flexibility to developers as they can reuse the same variable for different types of values. However, it also requires careful consideration to avoid potential bugs caused by unexpected changes in variable types.


## Duck Typing
Duck typing is a concept in Python where the type or class of an object is less important than the methods and attributes it provides. In other words, if an object walks like a duck and quacks like a duck, then it is considered as a duck.

This concept allows for flexible programming and is often associated with Python's "we don't care about the actual type, just what it can do" philosophy.

```python
# Duck Typing in Python
class Duck:
    def walk(self):
        print("Duck is walking")

    def quack(self):
        print("Duck is quacking")

class Person:
    def walk(self):
        print("Person is walking")

    def quack(self):
        print("Person is quacking")


def make_sound(obj):
    obj.quack()


duck = Duck()
person = Person()

make_sound(duck)   # Output: Duck is quacking
make_sound(person) # Output: Person is quacking
```

In the example above, we have two classes `Duck` and `Person`, both of which have `walk` and `quack` methods. The `make_sound` function does not care about the actual type of the object passed to it; it only checks if the object has a `quack` method and calls it.

This is an illustration of duck typing. As long as an object provides the required methods or attributes, it can be used interchangeably.

## Conclusion
Dynamic typing and duck typing are powerful features of Python that give developers the flexibility to write more expressive and concise code. Understanding these concepts allows you to leverage the full potential of Python and create robust and flexible applications.

References:
- [Python documentation on dynamic typing](https://docs.python.org/3.9/glossary.html#term-dynamic-typing)
- [Python documentation on duck typing](https://docs.python.org/3/glossary.html#term-duck-typing)