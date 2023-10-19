---
layout: post
title: "[python] Regular expressions in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

Regular expressions are a powerful tool for pattern matching and text manipulation. They allow you to search, find, and manipulate strings based on specific patterns. In Python, the `re` module provides functions to work with regular expressions. Let's dive into some common use cases and examples.

## Searching for a pattern

To search for a specific pattern in a string, you can use the `re.search()` function. It returns a match object if the pattern is found, otherwise it returns `None`. Here's an example:

```python
import re

pattern = r"apple"
text = "I love apples."

match = re.search(pattern, text)

if match:
    print("Pattern found!")
else:
    print("Pattern not found.")
```

In this example, the pattern is the word "apple" and the text we search in is "I love apples." The `re.search()` function finds the pattern in the text and the `match` object is not `None`, so the output will be "Pattern found!".

## Matching multiple occurrences

To find multiple occurrences of a pattern in a string, you can use the `re.findall()` function. It returns a list of all matches. Here's an example:

```python
import re

pattern = r"app"
text = "I love apples, especially apple pie."

matches = re.findall(pattern, text)

print(matches)
```

In this example, the pattern is the substring "app" and the text we search in is "I love apples, especially apple pie.". The `re.findall()` function finds all occurrences of "app" and the output will be `['app', 'app']`.

## Replacing pattern matches

Regular expressions can also be used to replace specific patterns in a string with new values. The `re.sub()` function is used for this purpose. Here's an example:

```python
import re

pattern = r"apple"
text = "I have an apple."

new_text = re.sub(pattern, "orange", text)

print(new_text)
```

In this example, the pattern is the word "apple" and the text we search in is "I have an apple.". The `re.sub()` function replaces all occurrences of "apple" with "orange", so the output will be "I have an orange.".

## Flags for case-insensitive matching

By default, regular expressions in Python are case-sensitive. However, you can use flags to perform case-insensitive matching. The `re.IGNORECASE` flag is used for this purpose. Here's an example:

```python
import re

pattern = r"apple"
text = "I love Apples."

match = re.search(pattern, text, re.IGNORECASE)

if match:
    print("Pattern found!")
else:
    print("Pattern not found.")
```

In this example, the pattern is the word "apple" and the text we search in is "I love Apples.". The `re.search()` function uses the `re.IGNORECASE` flag to perform a case-insensitive search, so the output will be "Pattern found!".

These are just a few examples of how regular expressions can be used in Python. They offer a powerful and flexible way to work with textual data and handle complex string matches. Refer to the [Python documentation for regular expressions](https://docs.python.org/3/library/re.html) for more details and advanced usage.