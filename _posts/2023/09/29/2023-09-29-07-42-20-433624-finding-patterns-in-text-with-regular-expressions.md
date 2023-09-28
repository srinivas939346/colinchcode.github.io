---
layout: post
title: "[python] Finding patterns in text with regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

Regular expressions (regex) are powerful tools for manipulating and searching for patterns in text. Whether you're a programmer, analyst, or data scientist, understanding regex can greatly enhance your text processing capabilities. In this blog post, we'll explore the basics of regex and learn how to use them in Python.

## Table of Contents
1. [Introduction to Regular Expressions](#introduction-to-regular-expressions)
2. [Matching Patterns](#matching-patterns)
3. [Character Classes](#character-classes)
4. [Quantifiers](#quantifiers)
5. [Groups and Capturing](#groups-and-capturing)
6. [Search and Replace](#search-and-replace)
7. [Conclusion](#conclusion)

## Introduction to Regular Expressions

A regular expression is a sequence of characters that defines a search pattern. It allows you to match, search, and manipulate text based on specific patterns. Regex patterns are defined using a combination of literal characters and metacharacters.

In Python, the `re` module provides functions for working with regular expressions. To get started, let's import the module:

```python
import re
```

## Matching Patterns

The most basic use of regular expressions is to match patterns within text. The `re.search()` function allows you to search for a pattern within a string. Here's an example:

```python
text = "Hello, world! This is a sample text."
pattern = r"world"
match = re.search(pattern, text)

if match:
    print("Pattern found!")
else:
    print("Pattern not found.")
```

The output will be "Pattern found!" since the word "world" exists in the `text` string.

## Character Classes

Character classes allow you to specify a set of characters that can match at a particular position in the pattern. For example, the character class `[aeiou]` matches any vowel. Here's how you can use character classes in Python:

```python
text = "The quick brown fox jumps over the lazy dog."
pattern = r"[aeiou]"
matches = re.findall(pattern, text)

print(matches)
```

The output will be `['e', 'u', 'i', 'o', 'o', 'u', 'o', 'e', 'o', 'e', 'a', 'o', 'u', 'o', 'o']`, which are all the vowels found in the `text` string.

## Quantifiers

Quantifiers specify the number of times a pattern should occur in order to be considered a match. Common quantifiers include `*` (zero or more occurrences), `+` (one or more occurrences), and `?` (zero or one occurrence). Here's an example:

```python
text = "aaaaaabbbbbbcccccc"
pattern = r"b+"
matches = re.findall(pattern, text)

print(matches)
```

The output will be `['bbbbbb']`, which is the longest sequence of consecutive "b" characters in the `text` string.

## Groups and Capturing

Groups allow you to capture parts of a match for further processing. You can define groups using parentheses. Here's an example:

```python
text = "My favorite fruits are apples, bananas, and oranges."
pattern = r"(apples|bananas|oranges)"
matches = re.findall(pattern, text)

print(matches)
```

The output will be `['apples', 'bananas', 'oranges']`, which are all the fruits mentioned in the `text` string.

## Search and Replace

The `re.sub()` function allows you to replace patterns found in a string with a specified value. Here's an example:

```python
text = "I love cats, but I also like dogs."
pattern = r"cats"
replacement = "dogs"
new_text = re.sub(pattern, replacement, text)

print(new_text)
```

The output will be "I love dogs, but I also like dogs."

## Conclusion

Regular expressions are a powerful tool for finding and manipulating patterns in text. In this blog post, we've covered the basics of regex in Python, including pattern matching, character classes, quantifiers, groups, and search-and-replace operations. With this knowledge, you can now apply regular expressions to a wide range of text-processing tasks in your projects.