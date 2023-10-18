---
layout: post
title: "[python] Generating combinations with Python generators"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to generate combinations using Python generators. Combinations are a set of items or elements selected from a larger set without any repetition. Python provides the `itertools` module which has a utility function called `combinations()` that allows us to generate combinations easily. However, in this post, we will implement our own combination generator using Python generators.

## What are Python generators?

Python generators are a type of iterator that generates values on the fly. They are defined using the `yield` keyword instead of the `return` keyword. Generators allow us to write code that produces a sequence of values without needing to store them all in memory at once. This can be extremely useful when dealing with large data sets and when we only need to process one value at a time.

## Implementing the combination generator

Let's first define the function signature for our combination generator:
```python
def combinations_generator(items, r):
```
- `items` - The iterable from which we want to generate combinations.
- `r` - The length of each combination.

Inside the generator function, we will use recursion to generate all possible combinations. The base case is when `r` is 0, in which case we yield an empty tuple. For each item in `items`, we recursively call the generator with the remaining items and `r-1`. We then prepend the current item to each combination and yield it.

Here's the implementation of the `combinations_generator()` function:

```python
def combinations_generator(items, r):
    if r == 0:
        yield ()
    else:
        for i in range(len(items)):
            item = items[i]
            remaining_items = items[i+1:]
            for c in combinations_generator(remaining_items, r-1):
                yield (item,) + c
```

## Using the combination generator

Now that we have implemented the combination generator, let's see how we can use it. 

To generate all combinations of length 2 from a list of items, we can simply iterate over the generator and print each combination:

```python
items = ['apple', 'banana', 'cherry', 'date']
combinations = combinations_generator(items, 2)

for combination in combinations:
    print(combination)
```

This will output:
```
('apple', 'banana')
('apple', 'cherry')
('apple', 'date')
('banana', 'cherry')
('banana', 'date')
('cherry', 'date')
```

## Conclusion

In this blog post, we learned how to generate combinations using Python generators. We implemented our own combination generator using recursion and the `yield` keyword. Python generators are a powerful tool for generating values on the fly without storing them all in memory at once. They allow us to process large data sets efficiently and lazily.