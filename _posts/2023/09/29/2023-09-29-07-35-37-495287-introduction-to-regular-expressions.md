---
layout: post
title: "[python] Introduction to regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

Regular expressions are a powerful tool for pattern matching and manipulation of text data. They provide a concise and flexible way to search, extract, and manipulate strings based on specific patterns.

In Python, regular expressions are supported through the `re` module. This module provides various functions and methods for working with regular expressions.

In this tutorial, we will cover the basics of regular expressions in Python and explore some common use cases.

## Table of Contents
1. [What are Regular Expressions?](#what-are-regular-expressions)
2. [Basic Pattern Matching](#basic-pattern-matching)
3. [Metacharacters and Escaping](#metacharacters-and-escaping)
4. [Quantifiers](#quantifiers)
5. [Character Classes](#character-classes)
6. [Grouping and Capturing](#grouping-and-capturing)
7. [Anchors](#anchors)
8. [Modifiers](#modifiers)
9. [Using Regular Expressions in Python](#using-regular-expressions-in-python)
10. [Conclusion](#conclusion)

## What are Regular Expressions?

A regular expression is a sequence of characters that defines a search pattern. It consists of regular characters and special characters called metacharacters. Metacharacters allow you to create more complex patterns by representing a group of characters or defining repetition.

Regular expressions can be used for tasks such as:
- Validating input data
- Searching for patterns in text
- Extracting specific information from text
- Replacing text with a different pattern

## Basic Pattern Matching

The most basic operation with regular expressions is pattern matching. You define a pattern and search for it in a given text. Here's a simple example:

```python
import re

text = "Hello, World!"
pattern = r"Hello"
match = re.search(pattern, text)
print(match.group())  # Output: Hello
```

In the example above, we use the `re.search()` function to search for the pattern `Hello` in the text. The `r` before the pattern string indicates a raw string, which allows backslashes to be treated as literal characters.

The `match` object returned by `re.search()` contains information about the match, and we can access the matched string using the `group()` method.

## Metacharacters and Escaping

Regular expressions use various metacharacters to define patterns. Some of the commonly used metacharacters are `.` (dot), `*` (asterisk), `+` (plus), `?` (question mark), `[ ]` (brackets), `{ }` (curly braces), `^` (caret), `$` (dollar sign), `|` (pipe), and `\` (backslash).

To match a metacharacter as a regular character, you need to escape it using a backslash `\`. For example:

```python
import re

text = "10 + 20 = 30"
pattern = r"\+"
match = re.search(pattern, text)
print(match.group())  # Output: +
```

In this example, the pattern `\+` matches the plus sign in the text. By escaping the plus sign, we treat it as a regular character rather than a metacharacter.

## Quantifiers

Quantifiers specify how many times a character or a group of characters should occur in a pattern. Some commonly used quantifiers are `*` (zero or more occurrences), `+` (one or more occurrences), `?` (zero or one occurrence), and `{n}` (exactly n occurrences).

For example:

```python
import re

text = "abcaaacde"
pattern = r"a+"
matches = re.findall(pattern, text)
print(matches)  # Output: ['a', 'aaa']
```

In this example, the pattern `a+` matches one or more occurrences of the letter 'a' in the text. The `re.findall()` function returns a list of all matches found.

## Character Classes

Character classes allow you to match any character from a set of characters. They are defined using square brackets `[ ]`.

For example:

```python
import re

text = "Hello, World!"
pattern = r"[aeiou]"
matches = re.findall(pattern, text, re.IGNORECASE)
print(matches)  # Output: ['e', 'o', 'o']
```

In this example, the pattern `[aeiou]` matches any vowel in the text, regardless of case (ignoring case using the `re.IGNORECASE` flag). The `re.findall()` function returns a list of all matches found.

## Grouping and Capturing

Grouping and capturing allow you to group parts of a pattern together and extract specific parts of the matched text. They are defined using parentheses `( )`.

For example:

```python
import re

text = "John Doe: 35 years old"
pattern = r"(\w+) (\w+): (\d+) years old"
match = re.search(pattern, text)
name = match.group(1)
age = match.group(3)
print(name)  # Output: John
print(age)   # Output: 35
```

In this example, the pattern `(\w+) (\w+): (\d+) years old` captures the name and age of a person. We can access the captured groups using the `group()` method, specifying the group index.

## Anchors

Anchors specify the position where a match should occur in the text. Some commonly used anchors are `^` (caret, matches the start of a line) and `$` (dollar sign, matches the end of a line).

For example:

```python
import re

text = "Hello, World!"
pattern = r"^Hello"
match = re.search(pattern, text)
print(match)  # Output: <re.Match object; span=(0, 5), match='Hello'>
```

In this example, the pattern `^Hello` matches the string only if it starts with "Hello". The `re.search()` function returns a match object if a match is found, otherwise it returns `None`.

## Modifiers

Modifiers are used to specify additional options for the regular expression search. They can be specified as an optional second argument in the `re.search()` function. Some common modifiers include `re.IGNORECASE` (ignore case), `re.MULTILINE` (multiline matching), and `re.DOTALL` (match any character, including newline).

For example:

```python
import re

text = "Hello, World!"
pattern = r"world"
match = re.search(pattern, text, re.IGNORECASE)
print(match)  # Output: <re.Match object; span=(7, 12), match='World'>
```

In this example, the pattern `world` is matched even though the case is different because we have used the `re.IGNORECASE` modifier.

## Using Regular Expressions in Python

As mentioned earlier, Python provides the `re` module for working with regular expressions. The most commonly used functions and methods are:

- `re.search(pattern, text)`: Search for a pattern in the text and return a match object.
- `re.findall(pattern, text)`: Find all occurrences of a pattern in the text and return a list of matches.
- `re.sub(pattern, replacement, text)`: Replace all occurrences of a pattern in the text with the replacement string.
- `re.split(pattern, text)`: Split the text based on the occurrences of a pattern and return a list of substrings.

## Conclusion

Regular expressions are a powerful tool for pattern matching and manipulation of text data. They allow you to search, extract, and manipulate strings based on specific patterns. Python provides the `re` module for working with regular expressions, with functions and methods like `re.search()`, `re.findall()`, `re.sub()`, and `re.split()`.

This tutorial covered the basics of regular expressions, including pattern matching, metacharacters, escaping, quantifiers, character classes, grouping, capturing, anchors, and modifiers. With this knowledge, you can start using regular expressions to solve various text processing tasks.

Remember to practice and experiment with different patterns to become more proficient in working with regular expressions.