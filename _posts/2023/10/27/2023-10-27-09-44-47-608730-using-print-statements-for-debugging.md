---
layout: post
title: "[python] Using print statements for debugging"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

When developing a program, it's inevitable to encounter bugs or issues that need to be addressed. Debugging is the process of locating and resolving these bugs. While Python provides several debugging tools and techniques, one of the simplest and most effective ways is using print statements.

## Why use print statements?

Print statements are a straightforward way to get information about the program's execution at specific points. They allow you to observe the values of variables, check if certain conditions are met, or track the flow of the program.

## Basic usage

The basic syntax for a print statement in Python is:

```python
print(value)
```

Here, `value` can be a variable, an expression, or even a string. The `print()` function takes in the value and displays it on the console.

Let's consider a simple example. Suppose you have the following code:

```python
def calculate_sum(a, b):
    sum = a + b
    print("The sum is:", sum)
    return sum

result = calculate_sum(5, 7)
```

In the example above, the `print()` statement displays the calculated sum on the console. This allows you to verify if the function is correctly adding the two numbers.

## Advanced usage

While basic print statements can be helpful, there are some additional techniques you can use to enhance your debugging process.

### Multiple values

You can pass multiple variables to the `print()` statement by separating them with commas. This can be useful to examine multiple variables in a single line:

```python
a = 5
b = 7
print("The values of a and b are:", a, b)
```

### String formatting

Python provides a powerful string formatting feature that allows you to construct complex output messages. By using string formatting, you can include variables or expressions within the print statement more elegantly:

```python
a = 5
b = 7
print(f"The sum of {a} and {b} is {a + b}")
```

The `f` character before the string indicates that it is a formatted string. Within the string, variables or expressions enclosed in curly braces `{}` will be replaced with their respective values.

### Logging module

While print statements are useful for simple debugging scenarios, if you need more advanced features like logging levels, file output, or filtering, the `logging` module is worth exploring. It provides a powerful debugging capability with more control over your debug information.

To use the `logging` module, you need to import it at the beginning of your program:

```python
import logging
```

Then, you can use various logging methods such as `logging.debug()`, `logging.info()`, `logging.warning()`, etc., to output debug information.

```python
import logging

logging.basicConfig(level=logging.DEBUG)

# Debug information
logging.debug("This is a debug message")

# Informational message
logging.info("This is an informational message")

# Warning message
logging.warning("This is a warning message")

# Error message
logging.error("This is an error message")
```

You can set the logging level to control which messages are displayed or saved to a file, making it a flexible way to debug your program.

## Conclusion

Using print statements is a simple yet effective technique for debugging your Python code. It allows you to observe the program's execution, inspect variable values, and track the flow of your code. However, for more advanced debugging scenarios, consider exploring the `logging` module, which provides additional features and customization options.