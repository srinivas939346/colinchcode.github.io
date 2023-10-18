---
layout: post
title: "[python] Difference between generators and functions in Python"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

Python provides two main ways to create iterable objects - generators and functions. While both of them can be used to iterate over a sequence of values, there are some key differences between them.

## Functions
In Python, functions are blocks of reusable code that perform a specific task. They take input arguments, execute the code inside the function body, and return a value (optional).

```python
def square_numbers(numbers):
    result = []
    for num in numbers:
        result.append(num ** 2)
    return result
```

In the above example, we define a function `square_numbers` that takes a list of numbers as input, iterates over each number, calculates its square, and stores the squared numbers in a list. Finally, the list is returned as the result.

## Generators
Generators are a type of iterable, similar to functions, but instead of returning a value immediately, they yield values one at a time. Generators use the `yield` keyword to pause the execution of the function and return a value to the caller. When the generator is called again, it resumes from where it left off.

```python
def square_numbers_generator(numbers):
    for num in numbers:
        yield num ** 2
```

In the above example, we define a generator function `square_numbers_generator` that behaves similar to the previous `square_numbers` function. However, instead of storing all the squared numbers in a list and returning it at once, it yields each squared number one at a time.

## Differences between generators and functions

1. **Memory efficiency**: Functions that return a list or any other data type store the entire sequence in memory. This can be memory-intensive, especially for large sequences. On the other hand, generators only store the current state of the iteration, yielding elements one at a time. They are memory-efficient and suitable for working with large datasets.

2. **Lazy evaluation**: Functions execute the entire code block and return the result immediately. In contrast, generators use lazy evaluation, meaning they evaluate and yield values only when requested. This makes them ideal for working with infinite sequences or when processing data in a streaming fashion.

3. **Iterability**: Functions can be called multiple times, and each call will execute the entire code block from the beginning. Generators, however, maintain their internal state and can be iterated over using a `for` loop or by calling the `next()` function. They remember where they left off, making them suitable for iterative processes.

4. **Execution flow**: Functions execute until they either reach the end of the code block or encounter a `return` statement. Generators, on the other hand, yield values and pause their execution until they are called again. This allows generators to perform computations incrementally and resume execution without losing their state.

In summary, functions and generators in Python serve different purposes. Functions are used to encapsulate and reuse blocks of code, whereas generators are useful for generating sequences of values efficiently, lazily, and in an iterative manner.