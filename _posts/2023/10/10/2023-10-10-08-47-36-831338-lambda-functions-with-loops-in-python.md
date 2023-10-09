---
layout: post
title: "[python] Lambda functions with loops in Python"
description: " "
date: 2023-10-10
tags: [python]
comments: true
share: true
---

In Python, lambda functions are anonymous functions that can be used inline without requiring a formal function declaration. They are commonly used in situations where a small, one-time function is needed.

In this blog post, we'll explore how to use lambda functions with loops in Python to perform certain operations on a collection of elements.

## Table of Contents
1. [Introduction](#introduction)
2. [Using lambda functions with loops](#using-lambda-functions-with-loops)
3. [Examples](#examples)
    - [1. Filtering even numbers](#example-1-filtering-even-numbers)
    - [2. Squaring numbers](#example-2-squaring-numbers)
4. [Conclusion](#conclusion)

## Introduction

Lambda functions are defined using the `lambda` keyword, followed by the function arguments and a colon, and then the expression to be evaluated.

```python
lambda arguments: expression
```

Lambda functions are particularly useful when you need a function for a short duration and don't want to define a separate named function. They can be passed as arguments to other functions, used in higher-order functions, or used with loops to perform operations on collections.

## Using lambda functions with loops

When using lambda functions with loops, you can leverage their concise syntax to perform operations on each element of a collection, such as filtering, transforming, or applying some logic.

The `map()` and `filter()` functions are commonly used with lambda functions to perform operations on collections. The `map()` function applies a given function to each element of a collection and returns an iterator with the results. The `filter()` function applies a given function to each element of a collection and returns an iterator with the elements that satisfy the given condition.

## Examples

Now, let's dive into a few examples to see how lambda functions can be used with loops.

### Example 1: Filtering even numbers

In this example, we have a list of numbers and we want to filter out the even numbers using a lambda function and the `filter()` function.

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
filtered_numbers = list(filter(lambda x: x % 2 == 0, numbers))
```

The lambda function `lambda x: x % 2 == 0` checks if a number is divisible by 2 (i.e., even). The `filter()` function applies this lambda function to each number in the `numbers` list and returns an iterator with the even numbers. Finally, we convert the iterator to a list using `list()`.

### Example 2: Squaring numbers

In this example, we have a list of numbers and we want to square each number using a lambda function and the `map()` function.

```python
numbers = [1, 2, 3, 4, 5]
squared_numbers = list(map(lambda x: x ** 2, numbers))
```

The lambda function `lambda x: x ** 2` squares each number. The `map()` function applies this lambda function to each number in the `numbers` list and returns an iterator with the squared numbers. Finally, we convert the iterator to a list using `list()`.

## Conclusion

Lambda functions with loops in Python provide a concise and efficient way to perform operations on collections. They can be used with functions like `filter()` and `map()` to filter, transform, or apply logic to each element in a collection. By leveraging lambda functions, you can write more expressive code and avoid the need for defining separate named functions for small, one-time operations.