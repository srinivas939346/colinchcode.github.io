---
layout: post
title: "[python] Closing a generator in Python"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

In Python, generators are a type of iterable that allows us to generate a sequence of values on the fly. One of the benefits of using generators is that they can save memory space by producing values one at a time instead of generating and storing all of them in memory.

Sometimes, we may want to prematurely stop a generator, before it completes generating all the values. In such cases, we need to properly close the generator to ensure any necessary cleanup operations are performed.

## Closing a Generator using the `close()` Method

To close a generator in Python, we can use the `close()` method. The `close()` method is a built-in method provided by generators that raises a `GeneratorExit` exception inside the generator, causing it to exit. 

Here's an example that demonstrates how to close a generator:

```python
def number_generator():
    try:
        for i in range(1, 10):
            yield i
    except GeneratorExit:
        print("Generator closed!")

# Creating the generator object
gen = number_generator()

# Iterating over the generator
for number in gen:
    print(number)
    if number == 5:
        gen.close()
```

In the code above, we define a generator function `number_generator()` that yields numbers from 1 to 9. Inside the generator function, we enclose the `yield` statement within a `try-except` block to catch the `GeneratorExit` exception.

We create a generator object `gen` by calling the `number_generator()` function. Then, we iterate over the generator using a `for` loop, printing each number. When the number becomes equal to 5, we close the generator using the `close()` method.

Upon closing the generator, the `GeneratorExit` exception is raised inside the generator and caught by the `except` block. In this example, we simply print a message indicating that the generator has been closed.

## Cleanup Operations using the `finally` Block

In some cases, we might want to perform cleanup operations before closing a generator. To do this, we can use a `finally` block.

A `finally` block is executed whether an exception occurs or not. This block allows us to define code that will always be executed before the generator is closed.

Here's an example that demonstrates using a `finally` block for cleanup operations:

```python
def file_reader(file_name):
    try:
        file = open(file_name, 'r')
        for line in file:
            yield line
    except GeneratorExit:
        print("Generator closed!")
    finally:
        file.close()
        print("File closed.")

# Creating the generator object
gen = file_reader("data.txt")

# Iterating over the generator
for line in gen:
    print(line.strip())

# Closing the generator
gen.close()
```

In this example, we define a generator function `file_reader(file_name)` that reads lines from a file. Inside the generator function, we open the file, iterate over its lines, and yield each line.

We enclose the file handling code within a `try` block to catch any exceptions. If a `GeneratorExit` exception occurs, indicating that the generator is being closed, we print a message indicating that the generator has been closed.

In the `finally` block, we close the file using the `close()` method and print a message indicating that the file has been closed.

## Conclusion

Closing a generator in Python using the `close()` method is a useful technique when we want to stop a generator prematurely. By properly closing a generator, we can ensure any necessary cleanup operations are performed before the generator is closed.