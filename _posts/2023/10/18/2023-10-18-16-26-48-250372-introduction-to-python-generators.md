---
layout: post
title: "[python] Introduction to Python generators"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

In Python, generators are a powerful concept that allows us to generate a sequence of values efficiently. They are useful when dealing with large datasets or when we need to iterate over a sequence of values one at a time.

## What are Generators?

Generators are defined using a special kind of function known as a generator function. These functions use the `yield` statement instead of the `return` statement to generate a value. When a generator function is called, it returns a generator object that can be iterated over.

Here's an example of a simple generator function that generates a sequence of numbers:

```python
def number_generator(n):
    for i in range(n):
        yield i
```

In the example above, the function `number_generator` generates numbers from 0 to `n-1`. Each time the `yield` statement is encountered, the function suspends its execution, remembers its state, and returns the value. When the generator is iterated over, it resumes its execution from the last state and produces the next value.

## Using Generators

To use a generator, we can iterate over it using a `for` loop or use the `next()` function to manually retrieve the next value. Let's see how to use the `number_generator` function:

```python
# Iterating over the generator using a for loop
for num in number_generator(5):
    print(num)

# Manually retrieving values using the next() function
gen = number_generator(3)
print(next(gen))  # prints 0
print(next(gen))  # prints 1
print(next(gen))  # prints 2
```

In the first example, we use a `for` loop to iterate over the generator and print each value. In the second example, we manually retrieve the values using the `next()` function.

## Benefits of Generators

Generators offer several benefits over traditional functions and lists:

1. Generators are memory efficient. They generate values on the fly, which means only one value is generated and stored in memory at a time, reducing memory usage.
2. Generators are lazy. They generate values only when needed, allowing for efficient handling of large datasets.
3. Generators are iterable. They can be used in any place that accepts an iterable, like `for` loops or list comprehensions.
4. Generators can be infinite. Since generators generate values on the fly, they can be used to represent infinite sequences.

## Conclusion

Generators in Python are a powerful tool for efficient and memory-friendly iteration. They provide a convenient way to generate sequences of values on-the-fly. By using `yield`, generator functions can suspend their execution and return values one at a time, making them ideal for working with large datasets or generating sequences that are not known in advance.