---
layout: post
title: "[python] How to use dictionary comprehension in Python?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

In Python, **dictionary comprehension** is a concise and efficient way to create new dictionaries from an iterable by specifying key-value pairs.

To use dictionary comprehension, you use a combination of curly braces `{}` and a `for` loop, similar to list comprehension. Here's the general syntax:

```python
{key_expression: value_expression for item in iterable}
```

Let's see some examples to understand how **dictionary comprehension** works.

## Creating a dictionary using dictionary comprehension

Suppose we have a list of numbers and we want to create a dictionary where the keys are the numbers and the values are their squares.

```python
numbers = [1, 2, 3, 4, 5]

squares = {num: num**2 for num in numbers}

print(squares)
```

Output:
```python
{1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
```

Here, the **key expression** `num` is the number itself, and the **value expression** `num**2` is the square of the number.

## Conditional dictionary comprehension

We can also include conditional statements in dictionary comprehension to filter the items. Let's see an example.

Suppose we have a list of numbers and we want to create a dictionary where the keys are the numbers and the values are their squares, but only for the even numbers.

```python
numbers = [1, 2, 3, 4, 5]

squares = {num: num**2 for num in numbers if num % 2 == 0}

print(squares)
```

Output:
```python
{2: 4, 4: 16}
```

Here, the if condition `num % 2 == 0` filters out the odd numbers, so only the even numbers and their squares are included in the dictionary.

## Conclusion

Dictionary comprehension is a powerful and efficient technique to create dictionaries in Python. It allows you to create dictionaries with a single line of code, making your code more concise and readable.

By using dictionary comprehension, you can easily transform an iterable into a dictionary by specifying the key-value pairs and optionally applying conditions. It's a handy tool to have in your Python toolbox!