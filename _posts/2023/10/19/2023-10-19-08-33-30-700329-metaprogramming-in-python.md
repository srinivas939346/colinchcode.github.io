---
layout: post
title: "[python] Metaprogramming in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

Metaprogramming is a technique where a program is capable of generating or modifying code at runtime. In Python, metaprogramming is made possible by its dynamic nature and the availability of powerful introspection and reflection capabilities. In this blog post, we will explore some of the metaprogramming techniques that Python offers.

## 1. Decorators

Decorators are a popular form of metaprogramming in Python. They allow you to modify the behavior of a function or a class by wrapping it with another function or class. Decorators are written using the `@` symbol.

Here's an example of a simple decorator that adds logging to a function:

```python
def logger(func):
    def wrapper(*args, **kwargs):
        print(f"Calling function: {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

@logger
def greet(name):
    print(f"Hello, {name}!")

greet("John")
```

Output:
```
Calling function: greet
Hello, John!
```

In the example above, the `logger` decorator is defined as a function that takes a function as its argument and returns a new function that wraps the original function. The `wrapper` function adds the logging functionality and calls the original function.

## 2. Metaclasses

Metaclasses are a powerful feature of Python that allows you to define the behavior of classes. They act as a blueprint for creating classes, similar to how classes are blueprints for creating objects. 

Here's an example of a simple metaclass that automatically adds a `__repr__` method to classes:

```python
class AutoRepr(type):
    def __init__(cls, name, bases, attrs):
        super().__init__(name, bases, attrs)
        def __repr__(self):
            return f"{self.__class__.__name__}({', '.join(f'{key}={getattr(self, key)}' for key in self.__dict__.keys())})"
        setattr(cls, "__repr__", __repr__)

class Person(metaclass=AutoRepr):
    def __init__(self, name, age):
        self.name = name
        self.age = age

person = Person("John", 25)
print(person)
```

Output:
```
Person(name=John, age=25)
```

In the example above, the `AutoRepr` metaclass is defined as a subclass of the built-in `type` metaclass. It overrides the `__init__` method to automatically add a `__repr__` method to classes that use the metaclass.

## 3. Runtime code generation

Python allows you to generate code dynamically at runtime using string manipulation or the `exec()` function. This can be useful in scenarios where you need to generate code based on certain conditions or input.

Here's an example of dynamically generating a function at runtime:

```python
def generate_function(func_name):
    code = f"def {func_name}():\n    print('Generated function')"
    exec(code)
    return locals()[func_name]

dynamic_func = generate_function("new_function")
dynamic_func()
```

Output:
```
Generated function
```

In the example above, the `generate_function` function generates a string of code representing a new function. The `exec()` function is used to execute the generated code and define the function at runtime. The `locals()` function is then used to retrieve the dynamically generated function by name.

## Conclusion

Metaprogramming in Python opens up a whole new world of possibilities for code generation and modification at runtime. Decorators, metaclasses, and runtime code generation are just a few of the techniques you can use to harness the power of metaprogramming in Python. By leveraging these techniques, you can write more flexible and expressive code that adapts to different scenarios.

References:
- [Python Metaprogramming: A Deep Dive](https://realpython.com/python-metaclasses/)
- [Understanding Python Decorators in 12 Easy Steps!](https://www.thecodeship.com/patterns/guide-to-python-function-decorators/)
- [Dynamic Python](https://www.dabeaz.com/pydata/PyData-toolz.html#)