---
layout: post
title: "[python] Combining generators with built-in Python functions"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

Generators are a powerful feature in Python that allow us to create iterators in a memory-efficient manner. They enable us to lazily generate values on the fly, which can be useful when dealing with large datasets or infinite sequences. On the other hand, Python provides a rich set of built-in functions that can operate on iterables, such as lists, tuples, and generators. In this article, we will explore how to combine generators with built-in Python functions.

## Table of Contents
- [Filtering with `filter()`](#filtering-with-filter)
- [Transforming with `map()`](#transforming-with-map)
- [Aggregating with `sum()`](#aggregating-with-sum)
- [Combining Multiple Generators with `zip()`](#combining-multiple-generators-with-zip)

## Filtering with `filter()`

The `filter()` function in Python allows us to create a new generator by filtering out elements from an existing iterable based on a given condition. We can pass a *predicate function* that returns `True` or `False` for each element, and only the elements for which the predicate function returns `True` will be included in the new generator.

Here's an example:

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Create a generator that filters out even numbers
even_numbers = filter(lambda x: x % 2 == 0, numbers)

for num in even_numbers:
    print(num)
```

Output:
```
2
4
6
8
10
```

In this example, we create a generator `even_numbers` that filters out even numbers from the `numbers` list. The `lambda` function checks whether a number is divisible by 2, and only the numbers that satisfy the condition are included in the new generator.

## Transforming with `map()`

The `map()` function in Python allows us to apply a given function to each element of an iterable and create a new generator containing the transformed elements. It takes a function and an iterable as input, and returns a generator that applies the function to each element of the iterable.

Here's an example:

```python
words = ["apple", "banana", "cherry"]

# Create a generator that converts the words to uppercase
uppercase_words = map(str.upper, words)

for word in uppercase_words:
    print(word)
```

Output:
```
APPLE
BANANA
CHERRY
```

In this example, we create a generator `uppercase_words` that applies the `str.upper()` function to each element of the `words` list. The function converts each word to uppercase and the resulting generator contains the transformed elements.

## Aggregating with `sum()`

The `sum()` function in Python allows us to calculate the sum of all elements in an iterable. While it can work directly with a list or tuple, it can also be combined with a generator to perform the sum operation.

Here's an example:

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Calculate the sum of all odd numbers
odd_sum = sum(filter(lambda x: x % 2 != 0, numbers))

print(odd_sum)
```

Output:
```
25
```

In this example, we directly combine the `filter()` function with `sum()` to calculate the sum of all odd numbers in the `numbers` list. The `filter()` function only includes odd numbers, and the `sum()` function calculates their sum.

## Combining Multiple Generators with `zip()`

The `zip()` function in Python allows us to combine multiple generators or iterables element-wise and create a new generator containing tuples of corresponding elements. It stops when the shortest iterable is exhausted.

Here's an example:

```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
cities = ["New York", "London", "Paris"]

# Combine multiple generators
combined_generator = zip(names, ages, cities)

for person in combined_generator:
    print(person)
```

Output:
```
("Alice", 25, "New York")
("Bob", 30, "London")
("Charlie", 35, "Paris")
```

In this example, we use `zip()` to combine the `names`, `ages`, and `cities` generators. Each tuple produced by the `zip()` function contains the corresponding elements from each generator.

## Conclusion

Combining generators with built-in Python functions can provide a concise and efficient way to process data. With functions like `filter()`, `map()`, `sum()`, and `zip()`, we can easily filter, transform, aggregate, and combine elements from generators or other iterables. Understanding how to use these functions effectively can greatly simplify the handling of data in Python.