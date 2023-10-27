---
layout: post
title: "[python] Debugging with step-by-step execution"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Debugging is an essential part of the software development process. It helps identify and fix issues in your code, ensuring that it runs smoothly and produces the expected results. One effective technique for debugging is step-by-step execution, which allows you to execute your code line by line and observe its behavior at each step.

In this blog post, we will explore how to perform step-by-step execution in Python using the built-in `pdb` module.

## Table of Contents
- [What is Step-by-Step Execution](#what-is-step-by-step-execution)
- [Setting Breakpoints](#setting-breakpoints)
- [Stepping Through the Code](#stepping-through-the-code)
- [Interacting with the Debugger](#interacting-with-the-debugger)
- [Exiting the Debugger](#exiting-the-debugger)
- [Conclusion](#conclusion)

## What is Step-by-Step Execution

Step-by-step execution allows you to control the flow of your code and observe the state of variables and objects at each step. It helps you identify the point where your code behaves unexpectedly or produces incorrect results. By executing your code line by line, you can track the changes and find the root cause of the problem efficiently.

## Setting Breakpoints

**Breakpoints** are specific lines in your code where you want the debugger to pause execution. They allow you to start stepping through your code from a specific point. In Python, you can set breakpoints using the `pdb.set_trace()` function from the `pdb` module.

Here's an example:

```python
import pdb

def calculate_sum(num1, num2):
    result = num1 + num2
    pdb.set_trace()
    return result

sum = calculate_sum(5, 10)
print(f"The sum is: {sum}")
```

In the code above, we import the `pdb` module and use the `set_trace()` function to set a breakpoint within the `calculate_sum()` function. When the code encounters this line, it will pause execution and launch the debugger.

## Stepping Through the Code

Once the debugger is launched, you can step through your code using various commands:

- **`n` (next)**: Executes the current line and moves to the next line.
- **`s` (step)**: Steps into a function call, allowing you to continue debugging within that function.
- **`c` (continue)**: Continues execution until the next breakpoint or the end of the program.

Here's an example of using step-by-step execution with the debugger:

```
> /path/to/script.py(5)calculate_sum()
-> return result
(Pdb) n
The sum is: 15
--Return--
> /path/to/script.py(5)calculate_sum()->15
-> return result
```

In the example above, we stepped to the next line using the `n` command, and the debugger executed the `return result` line. The output shows the result of the `calculate_sum()` function and continues to execute the remaining code.

## Interacting with the Debugger

While debugging, you can also interact with the debugger to inspect variables, objects, and execute any valid Python code:

- **`p` (print)**: Prints the value of a variable.
- **`l` (list)**: Shows the current line of code and a few lines of context.
- **`h` (help)**: Displays the list of available commands and their descriptions.

For example, you can print the value of a variable using the `p` command:

```
(Pdb) p result
15
```

The debugger allows you to pause the execution of your code at any point, print variables, and perform other debugging actions to identify and fix the issue efficiently.

## Exiting the Debugger

To exit the debugger and resume normal program execution, you can either press `q` or type `exit` in the debugger prompt.

## Conclusion

Step-by-step execution with the `pdb` module in Python provides an effective way to debug your code by allowing you to observe its behavior line by line. By setting breakpoints and stepping through the code, you can easily identify and fix issues in your program. Remember to use the commands available in the debugger to inspect variables and objects, further enhancing the debugging process.

References:
- [Python documentation on pdb](https://docs.python.org/3/library/pdb.html)
- [Real Python article on debugging with pdb](https://realpython.com/python-debugging-pdb/)