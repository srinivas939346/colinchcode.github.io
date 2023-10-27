---
layout: post
title: "[python] Debugging with assertions"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

As developers, we often encounter bugs in our code. Debugging is an essential part of the software development process. One useful tool for debugging is the **assertion** statement, which allows us to verify certain assumptions about our code.

## What is an Assertion?

In Python, an assertion is a statement that checks if a given condition is true. If the condition is true, nothing happens and the program continues execution as normal. However, if the condition is false, an **AssertionError** is raised, indicating that something unexpected has occurred.

Assertions are typically used to check for logical errors in our code during development and testing. They help us catch and correct these errors early on, making our code more robust.

## Using Assertions for Debugging

Assertions can be used as a powerful debugging tool. By placing assertions throughout our code, we can verify the correctness of our assumptions at runtime. If an assertion fails, it means that our assumption is incorrect, pointing us directly to the source of the issue.

Consider the following example:

```python
def divide(a, b):
    assert b != 0, "Cannot divide by zero!"
    return a / b
```

In this example, we have a `divide` function that divides two numbers. To ensure that the second argument is not zero (which would lead to a ZeroDivisionError), we use an assertion to check this condition. If the condition is false, the assertion error is raised with the specified error message.

## Enabling and Disabling Assertions

Assertions can be enabled or disabled depending on the environment in which the code is running. By default, Python has assertions enabled, but they can be disabled globally by using the `-O` or `-OO` command-line options. When assertions are disabled, all assertion statements are completely ignored, resulting in improved performance.

To enable or disable assertions at a specific point in your code, you can use the `__debug__` built-in variable. By default, `__debug__` is `True`, enabling assertions. Setting it to `False` will disable assertions specifically for that section of the code.

```python
def divide(a, b):
    if __debug__:
        assert b != 0, "Cannot divide by zero!"
    return a / b
```

## Conclusion

Assertions are a useful tool for debugging and ensuring the correctness of our code. By using assertions strategically, we can catch issues early on and improve the reliability of our software.

Remember to use assertions mainly during development and testing, as they are usually disabled in production environments for performance reasons.

References:
- [Python Documentation - Assertions](https://docs.python.org/3/reference/simple_stmts.html#the-assert-statement)