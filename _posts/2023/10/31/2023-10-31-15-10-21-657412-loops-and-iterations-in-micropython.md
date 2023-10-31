---
layout: post
title: "[python] Loops and iterations in MicroPython"
description: " "
date: 2023-10-31
tags: [python]
comments: true
share: true
---

MicroPython, a lean and efficient implementation of the Python 3 programming language, provides several ways to execute code repeatedly. Loops and iterations allow us to automate tasks and perform actions multiple times without writing redundant code.

In this article, we will explore the different types of loops available in MicroPython and see how they can be used for efficient and concise programming.

## Table of Contents
- [While Loop](#while-loop)
- [For Loop](#for-loop)
- [Nested Loops](#nested-loops)
- [Loop Control Statements](#loop-control-statements)

## While Loop
The `while` loop is a fundamental control flow statement in MicroPython (and in most programming languages). It repeatedly executes a block of code as long as a specified condition is true.

Here's an example of a while loop in MicroPython:

```python
counter = 0
while counter < 5:
    print("Counter: ", counter)
    counter += 1
```
Output:
```
Counter: 0
Counter: 1
Counter: 2
Counter: 3
Counter: 4
```

In this example, the `while` loop runs until the `counter` variable reaches a value of 5. The counter is incremented by 1 with each iteration.

## For Loop
The `for` loop is another commonly used loop in MicroPython. It iterates over a sequence (such as a list, tuple, or string), executing a specified block of code for each element in the sequence.

Here's an example of a for loop in MicroPython:

```python
fruits = ['apple', 'banana', 'cherry']
for fruit in fruits:
    print(fruit)
```
Output:
```
apple
banana
cherry
```

In this example, the `for` loop iterates over each element in the `fruits` list and prints it.

## Nested Loops
MicroPython supports nested loops, which are loops inside another loop. This is useful when we need to perform repetitive tasks with multiple levels of iteration.

Here's an example of a nested loop in MicroPython:

```python
for i in range(3):
    for j in range(2):
        print(i, j)
```
Output:
```
0 0
0 1
1 0
1 1
2 0
2 1
```

In this example, the outer loop iterates over the values 0, 1, and 2, while the inner loop iterates over the values 0 and 1. The `print` statement displays the combined values of `i` and `j`.

## Loop Control Statements
MicroPython provides loop control statements to modify the behavior of loops. These statements allow us to control when a loop should continue, break, or skip iterations.

The three loop control statements are:

- `continue`: Skips the rest of the current iteration and proceeds to the next one.
- `break`: Exits the loop entirely.
- `pass`: Does nothing and acts as a placeholder when no action is needed.

Here's an example of using the loop control statements in MicroPython:

```python
for i in range(5):
    if i == 2:
        continue
    if i == 4:
        break
    print(i)
```
Output:
```
0
1
3
```

In this example, the loop continues to the next iteration when `i` is equal to 2 because of the `continue` statement. It breaks out of the loop when `i` is equal to 4 due to the `break` statement.

## Conclusion
Loops and iterations are essential in any programming language, including MicroPython. While loops help us execute code as long as a condition is satisfied, for loops are useful for iterating over sequences. Moreover, MicroPython's support for nested loops and loop control statements further extends their capabilities.

By leveraging loops and iterations, we can automate repetitive tasks, process data efficiently, and write concise and clean code.

For more information on loops and iterations in MicroPython, refer to the [MicroPython documentation](https://docs.micropython.org/en/latest/) and experiment with different examples to deepen your understanding.