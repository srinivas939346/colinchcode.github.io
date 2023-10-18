---
layout: post
title: "[python] Nested generators in Python"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

Generators in Python are a powerful feature that allows lazy evaluation of data. They are used to create iterable objects with a memory-efficient approach. One interesting aspect of generators is the ability to nest them within each other. In this blog post, we'll explore how to work with nested generators in Python.

## Table of Contents

1. [Introduction to Generators](#introduction-to-generators)
2. [Nested Generators](#nested-generators)
3. [Example: Generating Prime Numbers](#example-generating-prime-numbers)
4. [Benefits of Nested Generators](#benefits-of-nested-generators)
5. [Conclusion](#conclusion)

## Introduction to Generators
Generators in Python can be created using the `yield` keyword within a function. They allow you to create a sequence of values on the fly, as opposed to generating all the values at once. This makes generators memory-efficient, especially when working with large datasets or infinite sequences.

## Nested Generators
In Python, generators can be nested within each other. This means that the `yield` statement can be used within another generator to create a sequence of values. This concept is also known as generator composition.

Nested generators can be useful when you want to apply a series of transformations or filters to a sequence of data. Each nested generator can perform a specific transformation or filtering operation, and the result can be piped into the next generator in the chain.

Here's an example of a nested generator:

```python
def generate_numbers():
    for i in range(10):
        yield i

def square_numbers(numbers):
    for num in numbers:
        yield num**2

def filter_even_numbers(numbers):
    for num in numbers:
        if num % 2 == 0:
            yield num

nested_generator = filter_even_numbers(square_numbers(generate_numbers()))

for num in nested_generator:
    print(num)
```

In this example, `generate_numbers()` generates a sequence of numbers from 0 to 9. The `square_numbers()` generator takes this sequence and yields the square of each number. Finally, the `filter_even_numbers()` generator filters out the even numbers from the squared sequence.

By chaining these generators using nested generator composition, we get a sequence of squared even numbers.

## Example: Generating Prime Numbers
Let's consider another example to demonstrate the power of nested generators in Python. We'll create a nested generator that generates prime numbers using the Sieve of Eratosthenes algorithm.

```python
def generate_numbers(start, end):
    for i in range(start, end + 1):
        yield i

def generate_primes(start, end):
    numbers = generate_numbers(start, end)
    while True:
        prime = next(numbers)
        yield prime
        numbers = (num for num in numbers if num % prime != 0)

nested_generator = generate_primes(2, 20)

for prime in nested_generator:
    print(prime)
```

In this example, the `generate_numbers()` generator generates a sequence of all numbers between the given start and end range. `generate_primes()` takes this sequence and repeatedly yields the next prime number using the Sieve of Eratosthenes algorithm. The primes are obtained by filtering out all the multiples of the current prime number from the remaining numbers in the sequence.

## Benefits of Nested Generators
Using nested generators provides several benefits:
- **Modularity**: Nested generators allow you to break complex tasks into smaller, more manageable generators. Each generator can handle a specific step or transformation, making the code more modular and easier to understand.
- **Memory Efficiency**: By using generators, you can avoid loading large datasets into memory all at once. Instead, data is generated on-the-fly as needed, reducing memory consumption.
- **Lazy Evaluation**: Generators follow the "lazy evaluation" approach, which means they evaluate values on demand. This can be useful when working with infinite sequences or when you want to delay computation until it is needed.

## Conclusion
Nested generators are a powerful feature in Python that allows you to build complex data processing pipelines in a modular and memory-efficient way. By chaining generators together, you can easily transform and filter sequences of data. Understanding how to work with nested generators opens up the door to writing more efficient and scalable code in Python.

**References:**
- [Python Generators](https://docs.python.org/3/glossary.html#term-generator)
- [Generator Expressions](https://docs.python.org/3/glossary.html#term-generator-expression)