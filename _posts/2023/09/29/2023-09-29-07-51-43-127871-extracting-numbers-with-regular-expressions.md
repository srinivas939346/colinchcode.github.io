---
layout: post
title: "[python] Extracting numbers with regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

Regular expressions are a powerful tool for pattern matching and extraction in text. They can be very handy when you need to extract numbers from a string in Python. In this blog post, we will explore how to use regular expressions to extract numbers effectively.

## Table of Contents
1. [Introduction](#introduction)
2. [Using the `re` module](#using-the-re-module)
3. [Extracting integers](#extracting-integers)
4. [Extracting floating-point numbers](#extracting-floating-point-numbers)
5. [Extracting decimal numbers](#extracting-decimal-numbers)
6. [Conclusion](#conclusion)

## Introduction <a name="introduction"></a>

Regular expressions are a sequence of characters that define a search pattern. They provide a concise and flexible way to match and extract specific patterns from a given string. Python provides the `re` module for working with regular expressions.

## Using the `re` module <a name="using-the-re-module"></a>

To use regular expressions in Python, we first need to import the `re` module. By using the functions provided by this module, we can perform various operations like pattern matching, substitution, and extraction.

```python
import re
```

## Extracting integers <a name="extracting-integers"></a>

If you want to extract integers from a string, you can use the `\d+` pattern, where `\d` matches any digit and `+` matches one or more occurrences. Here's an example:

```python
import re

s = "I have 10 apples and 5 bananas."
integers = re.findall(r'\d+', s)
print(integers)  # Output: ['10', '5']
```

The `re.findall()` function returns a list of all the matched patterns found in the string.

## Extracting floating-point numbers <a name="extracting-floating-point-numbers"></a>

To extract floating-point numbers, you can use the pattern `[+-]?\d+\.\d+`, where `[+-]?` matches an optional sign, `\d+` matches one or more digits, and `\.` matches the decimal point. Here's an example:

```python
import re

s = "The temperature is -3.5 degrees Celsius."
floats = re.findall(r'[+-]?\d+\.\d+', s)
print(floats)  # Output: ['-3.5']
```

## Extracting decimal numbers <a name="extracting-decimal-numbers"></a>

If you want to extract decimal numbers with optional commas, you can use the pattern `[+-]?\d{1,3}(,\d{3})*\.\d+`. In this pattern, `[+-]?` matches an optional sign, `\d{1,3}` matches one to three digits, `(,\d{3})*` matches zero or more occurrences of comma separated groups of three digits, and `\.\d+` matches the decimal part. Here's an example:

```python
import re

s = "The total amount is -$1,234,567.89."
decimals = re.findall(r'[+-]?\d{1,3}(,\d{3})*\.\d+', s)
print(decimals)  # Output: ['-1,234,567.89']
```

## Conclusion <a name="conclusion"></a>

Regular expressions are a powerful tool for extracting numbers from strings in Python. By using the `re` module and understanding different patterns, you can easily extract integers, floating-point numbers, or decimal numbers from any given text. Remember to import the `re` module, define your desired pattern, and use functions like `re.findall()` to efficiently extract the desired numbers.