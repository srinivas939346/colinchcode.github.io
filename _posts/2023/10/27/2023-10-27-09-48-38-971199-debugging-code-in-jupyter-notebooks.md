---
layout: post
title: "[python] Debugging code in Jupyter notebooks"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Jupyter notebooks are a popular tool for data analysis and interactive coding in Python. However, debugging code in notebooks can sometimes be challenging, as it requires a different approach compared to traditional text editors or Integrated Development Environments (IDEs).

In this blog post, we will explore some techniques and tips for effectively debugging code in Jupyter notebooks.

## Table of Contents
- [Introduction](#introduction)
- [Importing the debug module](#importing-the-debug-module)
- [Setting breakpoints](#setting-breakpoints)
- [Stepping through code](#stepping-through-code)
- [Inspecting variables](#inspecting-variables)
- [Handling exceptions](#handling-exceptions)
- [Conclusion](#conclusion)

## Introduction

Debugging is the process of identifying and fixing errors or bugs in your code. In Jupyter notebooks, we have the advantage of being able to execute code cells interactively, which makes it easier to identify and fix issues.

## Importing the debug module

Jupyter notebooks provide a built-in `debug` module that can be used for debugging purposes. To enable debugging mode, we need to import this module in our notebook. We can do this by running the following code:

``` python
import debugpy
debugpy.listen(5678)
```

## Setting breakpoints

In order to debug code in Jupyter notebooks, we need to set breakpoints at specific lines where we suspect there might be an issue. To set a breakpoint, we can make use of the `debugpy.breakpoint()` function. This function acts as a signal, indicating that the debugger should pause execution at that point.

Here's an example of how to set a breakpoint in a Jupyter notebook code cell:

``` python
import debugpy
debugpy.listen(5678)

# Set breakpoint
debugpy.breakpoint()

# Code to be debugged
...
```

## Stepping through code

Once we have set breakpoints in our code, we can start stepping through the code line by line to understand its behavior. To do this, we can run the cell containing the code and it will stop at the breakpoint.

To proceed to the next line of code, we can use the **step over** functionality, which can be accessed by clicking the **|>|** button in the notebook toolbar. This will execute the current line and move to the next line.

## Inspecting variables

While debugging, it's often helpful to inspect the values of variables at certain points in the code. In Jupyter notebooks, we can simply print out the variable values by using the `print()` function or by writing the variable name directly in a code cell.

Alternatively, we can also make use of the `debugpy.breakpoint()` function to pause execution at a specific line and inspect the variable values using the notebook's variable explorer.

## Handling exceptions

When debugging code in Jupyter notebooks, it's common to encounter exceptions and errors. To handle these exceptions, we can enclose the code that might raise an exception in a `try-except` block. Within the `except` block, we can use the `debugpy.post_mortem()` function to enter a post-mortem debugging session and inspect the error's details.

Here's an example of how to handle exceptions in a Jupyter notebook code cell:

``` python
import debugpy
debugpy.listen(5678)

try:
    # Code that might raise an exception
    ...
except Exception as e:
    debugpy.post_mortem()
```

## Conclusion

Debugging code in Jupyter notebooks can be made easier with the use of the built-in `debug` module. By setting breakpoints, stepping through code, inspecting variables, and handling exceptions, we can effectively identify and fix issues in our code. This allows us to develop and debug code in an iterative and interactive manner, making Jupyter notebooks a powerful tool for data analysis and development.