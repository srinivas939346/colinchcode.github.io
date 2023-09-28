---
layout: post
title: "[python] Predefined character classes in regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

In Python, regular expressions are supported through the `re` module. Here, we will explore some of the commonly used predefined character classes in regular expressions:

- `\d`: Matches any decimal digit (0-9). This is equivalent to the character class `[0-9]`.
- `\D`: Matches any non-digit character. This is equivalent to the character class `[^0-9]`.
- `\w`: Matches any alphanumeric character (a-z, A-Z, 0-9, and underscore `_`). This is equivalent to the character class `[a-zA-Z0-9_]`.
- `\W`: Matches any non-alphanumeric character. This is equivalent to the character class `[^a-zA-Z0-9_]`.
- `\s`: Matches any whitespace character (space, tab, newline, etc.).
- `\S`: Matches any non-whitespace character.
- `.`: Matches any character except a newline character.

Here's a simple example that demonstrates the usage of predefined character classes:

```python
import re

text = "Hello, 123 world!"

# Matching all digits
matches = re.findall(r'\d', text)
print(matches)  # Output: ['1', '2', '3']

# Matching all non-digits
matches = re.findall(r'\D', text)
print(matches)  # Output: ['H', 'e', 'l', 'l', 'o', ',', ' ', ' ', 'w', 'o', 'r', 'l', 'd', '!']

# Matching all word characters
matches = re.findall(r'\w', text)
print(matches)  # Output: ['H', 'e', 'l', 'l', 'o', '1', '2', '3', 'w', 'o', 'r', 'l', 'd']

# Matching all non-word characters
matches = re.findall(r'\W', text)
print(matches)  # Output: [',', ' ', ' ', '!']

# Matching all whitespace characters
matches = re.findall(r'\s', text)
print(matches)  # Output: [' ', ' ']
```

Predefined character classes simplify the process of writing regular expressions by providing a concise way to match commonly used sets of characters. Understanding and using these character classes can make your regular expressions more powerful and efficient. Experiment with these character classes in your own regular expressions to perform complex pattern matching and text manipulation tasks.