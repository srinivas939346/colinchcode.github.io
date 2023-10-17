---
layout: post
title: "[python] Use of whitespace around operators and brackets in PEP 8"
description: " "
date: 2023-10-17
tags: [python]
comments: true
share: true
---

In Python, maintaining consistent coding style is important for readability and maintainability of the code. PEP 8 is the official style guide for Python code, and it provides guidelines for various aspects of coding style, including the use of whitespace around operators and brackets.

## Whitespace Around Operators

PEP 8 recommends using whitespace around operators to improve readability. Here are the general rules:

- **Binary Operators**: Use a single space before and after binary operators, such as addition, subtraction, multiplication, division, assignment, etc.

  ```python
  x = y + z
  a = b * c
  ```

- **Assignment Operators**: Use a single space before and after assignment operators to improve clarity.

  ```python
  result = 10
  count += 1
  ```

- **Comparisons**: Use a single space before and after comparison operators for better readability.

  ```python
  if x == y:
      print("x is equal to y")
  ```

- **Logical Operators**: Use a single space before and after logical operators, such as `and`, `or`, and `not`.

  ```python
  if x > 10 and y < 20:
      print("Both conditions are true")
  ```

## Whitespace Around Brackets

PEP 8 also provides guidelines for using whitespace around brackets. Here are the rules:

- **Function Calls**: Don't use whitespace between a function name and the opening parenthesis. Use a single space between arguments.

  ```python
  print("Hello, world!")  # correct

  print ("Hello, world!")  # incorrect
  ```

- **Function Definitions**: Use the same spacing rules as function calls.

  ```python
  def add_numbers(a, b):
      return a + b

  def multiply_numbers(a, b):
      return a * b
  ```

- **Lists, Tuples, and Dictionaries**: Use a single space after commas in lists, tuples, and dictionaries for clarity.

  ```python
  my_list = [1, 2, 3, 4]
  my_tuple = (10, 20, 30)
  my_dict = {"name": "John", "age": 30}
  ```

Following these whitespace conventions not only makes the code consistent but also helps with readability and understanding. It is essential to adhere to these guidelines to make your code more professional and maintainable.

For more detailed information, you can refer to the official PEP 8 style guide: [PEP 8 -- Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/).