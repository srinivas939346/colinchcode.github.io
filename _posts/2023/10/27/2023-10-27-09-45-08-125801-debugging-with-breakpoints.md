---
layout: post
title: "[python] Debugging with breakpoints"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

When working on a complex Python program, it is common to encounter bugs or errors that need to be investigated. One of the most effective ways to debug such issues is by using breakpoints. Breakpoints allow you to pause the execution of your program at specific points, making it easier to analyze the state of variables and step through the code to find the source of the problem.

## Setting breakpoints

To set a breakpoint in Python, you can make use of the `pdb` (Python Debugger) module. Simply import it at the beginning of your script:

```python
import pdb
```

Next, you can choose the location in your code where you want the program to pause:

```python
pdb.set_trace()
```

The `set_trace()` function acts as a breakpoint marker and will halt the execution at that point.

## Debugging workflow

Once the program is paused at a breakpoint, you can interact with the debugger using several commands:

- `n` - execute the next line
- `s` - step into a function call
- `r` - continue until the current function returns
- `c` - continue execution until the next breakpoint or the end of the program
- `q` - quit the debugger

While the program is paused, you can also inspect the values of variables by simply typing their names and pressing enter.

## Example

Let's say we have a simple program that calculates the factorial of a number. However, there seems to be an issue with our implementation. We can use breakpoints to investigate the problem.

```python
import pdb

def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n-1)

pdb.set_trace()

result = factorial(5)
print(result)
```

When running the program, it will pause at the `set_trace()` line. From there, you can use the available commands to step through the code and observe the variables' values.

## Conclusion

Using breakpoints in Python allows you to effectively debug your code by pausing the execution at specific points and inspecting variables' values. It is an essential tool in the debugging process, helping you identify and fix issues in your code more efficiently.

For more information on Python debugging, you can refer to the official [Python documentation on PDB](https://docs.python.org/3/library/pdb.html).