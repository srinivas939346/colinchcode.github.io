---
layout: post
title: "[python] Conditional statements in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

Conditional statements in Python are used to make decisions based on a certain condition or set of conditions. These statements allow the program to execute different code blocks depending on whether a condition is true or false. In this article, we will discuss the different types of conditional statements in Python.

### if statement

The `if` statement is the most basic type of conditional statement. It allows you to execute a block of code only if a certain condition is true. Here's the syntax of an `if` statement:

```python
if condition:
    # code to be executed if the condition is true
```

The `condition` is an expression that evaluates to either true or false. If the condition is true, the code block indented under the `if` statement will be executed. Otherwise, it will be skipped.

### Example:

```python
x = 10

if x > 5:
    print("x is greater than 5")
```

In this example, since the condition `x > 5` is true (`10` is greater than `5`), the code inside the `if` block will be executed, and the output will be `x is greater than 5`.

### if-else statement

The `if-else` statement allows you to execute one block of code if the condition is true, and another block of code if the condition is false. Here's the syntax of an `if-else` statement:

```python
if condition:
    # code to be executed if the condition is true
else:
    # code to be executed if the condition is false
```

### Example:

```python
x = 3

if x > 5:
    print("x is greater than 5")
else:
    print("x is less than or equal to 5")
```

In this example, since the condition `x > 5` is false (`3` is not greater than `5`), the code inside the `else` block will be executed, and the output will be `x is less than or equal to 5`.

### if-elif-else statement

The `if-elif-else` statement allows you to check multiple conditions in sequence and execute different code blocks based on the first condition that evaluates to true. Here's the syntax of an `if-elif-else` statement:

```python
if condition1:
    # code to be executed if condition1 is true
elif condition2:
    # code to be executed if condition1 is false and condition2 is true
else:
    # code to be executed if both condition1 and condition2 are false
```

You can have multiple `elif` (short for "else if") blocks between the initial `if` and the final `else`. The conditions are evaluated in order, and the first one that is true will trigger the execution of the corresponding code block.

### Example:

```python
x = 3

if x > 5:
    print("x is greater than 5")
elif x > 0:
    print("x is greater than 0")
else:
    print("x is less than or equal to 0")
```

In this example, since the first condition `x > 5` is false, Python moves on to the next condition `x > 0`. Since this condition is true (`3` is greater than `0`), the code inside the corresponding `elif` block will be executed, and the output will be `x is greater than 0`.

Conditional statements are crucial in programming as they allow us to control the flow of our code based on specific conditions. By using `if`, `if-else`, and `if-elif-else` statements, you can create dynamic programs that adapt to different situations.

For more information on conditional statements in Python, you can refer to the official Python documentation [here](https://docs.python.org/3/tutorial/controlflow.html#if-statements).