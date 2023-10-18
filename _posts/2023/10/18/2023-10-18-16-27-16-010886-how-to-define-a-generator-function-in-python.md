---
layout: post
title: "[python] How to define a generator function in Python"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

In Python, generator functions are a powerful tool that allow you to create iterators in a more elegant and memory-efficient way. A generator function is defined using the `yield` keyword, which makes it possible to control the flow of execution and generate a series of values on the fly.

To define a generator function in Python, follow these steps:

1. Start by using the `def` keyword to define a function as you would with any other Python function.
2. Inside the function body, use the `yield` keyword followed by the value you want to yield. This will pause the execution of the function and return the value to the caller.
3. You can use the `yield` keyword multiple times in a generator function. Each time the function encounters a `yield` statement, it will return the value specified and then continue execution from where it left off.
4. The function will continue to yield values until it either encounters a `return` statement or reaches the end of the function body.

Here's an example of a simple generator function that yields a sequence of even numbers:

```python
def even_numbers(n):
    for i in range(n):
        if i % 2 == 0:
            yield i
```

In this example, calling `even_numbers(10)` will not immediately execute the function. Instead, it will return a generator object. To retrieve the values, you can use a loop or convert the generator object to a list:

```python
for number in even_numbers(10):
    print(number)
```

This will output the numbers 0, 2, 4, 6, and 8.

Generator functions are especially useful when dealing with large datasets or scenarios where you want to generate values dynamically without needing to store them all in memory at once. By using generators, you can optimize memory usage and increase overall performance.

Keep in mind that generator functions will not execute any code until you iterate over them or call a specific method such as `next()`. This lazy evaluation makes them a great choice for scenarios where you want to generate and process data on-demand.

For more information, you can refer to the [official Python documentation on generators](https://docs.python.org/3/tutorial/classes.html#generators).