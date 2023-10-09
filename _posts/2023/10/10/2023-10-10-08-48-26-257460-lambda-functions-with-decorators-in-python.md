---
layout: post
title: "[python] Lambda functions with decorators in Python"
description: " "
date: 2023-10-10
tags: [python]
comments: true
share: true
---

Decorators in Python allow you to modify the behavior of functions or classes. They provide a way to wrap or modify the existing functionality without permanently modifying the original code. Lambda functions, on the other hand, are anonymous functions that do not require a def statement and can be defined inline.

In this blog post, we will explore how to use lambda functions with decorators in Python, and how they can be powerful tools in extending and modifying the behavior of your code.

## What is a decorator?

A decorator in Python is a design pattern that allows you to modify the behavior of a function or class without changing its source code. It wraps the original function in another function, and provides additional functionality before or after the original function is called.

Decorators are often used for implementing cross-cutting concerns such as logging, caching, security, and performance monitoring.

## Using lambda functions with decorators

Lambda functions can be used in combination with decorators to create concise and expressive code. Let's see an example of how to use a lambda function as a decorator:

```python
def logger_decorator(func):
    def wrapper(*args, **kwargs):
        print(f"Logging: Calling function {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

@logger_decorator
def greet(name):
    return f"Hello, {name}!"

print(greet("John"))
```

In the example above, we have defined a decorator called `logger_decorator` using a lambda function. The decorator takes a function as an argument, and returns a new function `wrapper` that wraps the original function.

The `wrapper` function logs a message before calling the original function, and returns the result of the original function. We then use the `@logger_decorator` syntax to apply the decorator to the `greet` function.

When we run the code, it will output:

```
Logging: Calling function greet
Hello, John!
```

As you can see, the lambda function allows us to define the `logger_decorator` in a concise manner.

## Handling arguments with lambda functions

Lambda functions can also handle arguments when used as decorators. Let's modify our previous example to add an argument to the decorator:

```python
def logger_decorator(level):
    def actual_decorator(func):
        def wrapper(*args, **kwargs):
            print(f"Logging ({level}): Calling function {func.__name__}")
            return func(*args, **kwargs)
        return wrapper
    return actual_decorator

@logger_decorator(level="INFO")
def greet(name):
    return f"Hello, {name}!"

print(greet("John"))
```

In this updated code, we have added an argument to the `logger_decorator` lambda function, which allows us to specify the logging level. The decorator now returns another lambda function `actual_decorator`, which takes the original function as an argument and returns the `wrapper` function.

We then use the `@logger_decorator(level="INFO")` syntax to apply the decorator with the specified logging level to the `greet` function.

When we run the modified code, it will output:

```
Logging (INFO): Calling function greet
Hello, John!
```

## Conclusion

Lambda functions provide a convenient way to create decorators in Python. They allow us to define concise and expressive code that can modify the behavior of functions or classes without permanently modifying the original code.

By combining lambda functions with decorators, we can create powerful tools to extend and modify the behavior of our Python code.