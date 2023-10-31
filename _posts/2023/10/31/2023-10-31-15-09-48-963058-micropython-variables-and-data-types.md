---
layout: post
title: "[python] MicroPython variables and data types"
description: " "
date: 2023-10-31
tags: [python]
comments: true
share: true
---

In MicroPython, variables are used to store data that can be accessed and manipulated throughout the program. Like other programming languages, MicroPython supports various data types to represent different kinds of values. In this blog post, we will explore the different data types available in MicroPython and how to work with variables.

### Integer

An integer is a whole number without a fractional part. In MicroPython, you can assign an integer value to a variable as follows:

```python
x = 10
```

### Float

A float is a number with both an integer and fractional part. In MicroPython, you can assign a float value to a variable as follows:

```python
y = 3.14
```

### String

A string is a sequence of characters enclosed in single or double quotes. You can assign a string value to a variable as follows:

```python
name = 'MicroPython'
```

### Boolean

A boolean represents a binary value, either `True` or `False`. In MicroPython, you can assign a boolean value to a variable as follows:

```python
is_true = True
```

### List

A list is an ordered collection of values, enclosed in square brackets and separated by commas. Each value in the list can be of any data type. You can assign a list to a variable as follows:

```python
numbers = [1, 2, 3, 4, 5]
```

### Tuple

A tuple is an ordered collection of values, enclosed in parentheses and separated by commas. Like lists, each value in the tuple can be of any data type. However, unlike lists, tuples are immutable, meaning their values cannot be changed. You can assign a tuple to a variable as follows:

```python
colors = ('red', 'green', 'blue')
```

### Dictionary

A dictionary is an unordered collection of key-value pairs, enclosed in curly braces. Keys are unique identifiers, and their corresponding values can be of any data type. You can assign a dictionary to a variable as follows:

```python
person = {'name': 'John', 'age': 30, 'city': 'New York'}
```

### Conclusion

In this blog post, we covered the different data types available in MicroPython, including integers, floats, strings, booleans, lists, tuples, and dictionaries. Understanding these data types is essential for writing efficient and effective MicroPython code. Feel free to explore more about each data type and experiment with them in your MicroPython projects.

**References:**
- [MicroPython Documentation](https://docs.micropython.org/en/latest/)