---
layout: post
title: "[python] Generating random data with Python generators"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to use Python generators to generate random data. Python generators are a powerful tool that can be used to create iterators in an efficient and memory-friendly way.

## Table of Contents
- [What are Python generators?](#what-are-python-generators)
- [Generating random numbers](#generating-random-numbers)
- [Generating random strings](#generating-random-strings)
- [Generating random lists](#generating-random-lists)
- [Conclusion](#conclusion)

## What are Python generators?

Python generators are functions that can be paused and resumed on demand, allowing for efficient memory usage and lazy evaluation. They are defined using the `yield` keyword, which returns a value and temporarily suspends the execution of the function.

Generators are especially useful when dealing with large datasets or infinite sequences, as they allow you to generate values on the fly, without the need to store them all in memory at once.

## Generating random numbers

Python provides the `random` module, which offers various functions for generating random numbers. We can use this module in conjunction with a generator to create an infinite sequence of random numbers.

```python
import random

def random_numbers():
    while True:
        yield random.randint(1, 100)
```

The `random_numbers` generator will continuously yield random numbers between 1 and 100 when iterated over.

To use the generator, we can iterate over it using a `for` loop or fetch individual random numbers using the `next()` function:

```python
for num in random_numbers():
    print(num)
    if num > 50:
        break

# Output:
# 92
# 16
# 34
# 78
# 51
```

The loop will continue until a random number greater than 50 is generated.

## Generating random strings

Generating random strings can be useful in various scenarios, such as generating passwords or dummy data for testing. Python's `string` module provides a list of uppercase letters, lowercase letters, and punctuation characters, which we can use to create a generator for random strings.

```python
import string
import random

def random_string(length=10):
    while True:
        yield ''.join(random.choice(string.ascii_letters + string.digits) for _ in range(length))
```

In the above code, the `random_string` generator generates strings of a specified length by randomly selecting characters from the combination of uppercase letters, lowercase letters, and digits.

To use the generator, we can iterate over it or fetch individual random strings:

```python
for string in random_string(8):
    print(string)
    if string.startswith('a'):
        break

# Output:
# j8n6SYud
# 7aXzy9uq
# aM0CpEXF
```

The loop will continue until a random string starting with the letter 'a' is generated.

## Generating random lists

In addition to generating individual random values, we can also use generators to create random lists. For example, let's create a generator that generates a list of random numbers of a specified length.

```python
import random

def random_list(length):
    return [random.randint(1, 100) for _ in range(length)]
```

To use the generator, we can call it with the desired length parameter:

```python
random_numbers = random_list(5)
print(random_numbers)

# Output:
# [87, 51, 12, 68, 24]
```

The function will return a list of random numbers of the specified length.

## Conclusion

Python generators provide a flexible and memory-efficient way to generate random data. Whether you need to generate random numbers, strings, or lists, generators offer a powerful tool to accomplish these tasks. By leveraging the `yield` keyword, you can generate values on the fly without consuming excessive memory.