---
layout: post
title: "[python] Using lambda functions with map() function in Python"
description: " "
date: 2023-10-10
tags: [python]
comments: true
share: true
---

In Python, the `map()` function is a built-in function that allows you to apply a given function to each item of an iterable and return a new iterable with the results.

A lambda function, also known as an anonymous function, is a small function without a name that is defined inline. It is commonly used when you need a simple function that will only be used once.

The `map()` function, when combined with lambda functions, provides a concise way to apply a function to each item of a list, tuple, or any other iterable.

## Syntax

The syntax for using `map()` function with lambda functions is as follows:

```python
map(lambda argument: expression, iterable)
```

Here, `lambda argument: expression` represents the lambda function, and `iterable` is the object on which the function will be applied.

## Example

Let's say we have a list of numbers and we want to double each number in the list using a lambda function with `map()`.

Here's an example code snippet that demonstrates how to achieve this:

```python
numbers = [1, 2, 3, 4, 5]

doubled_numbers = list(map(lambda x: x * 2, numbers))

print(doubled_numbers)
```

Output:
```
[2, 4, 6, 8, 10]
```

In the above example, we define a lambda function `lambda x: x * 2` that takes an argument `x` and returns `x * 2`. We apply this lambda function to each item of the `numbers` list using the `map()` function. The result is a new list `doubled_numbers` with each number doubled.

The `map()` function returns an iterable, so we convert it to a list using the `list()` function to display the output in a readable format.

## Conclusion

Using lambda functions with the `map()` function in Python can help you perform operations on iterables in a concise and efficient way. It allows you to apply a given function to each item of an iterable and collect the results in a new iterable. This combination of functions is especially useful when you need to transform or manipulate data in a single line of code.