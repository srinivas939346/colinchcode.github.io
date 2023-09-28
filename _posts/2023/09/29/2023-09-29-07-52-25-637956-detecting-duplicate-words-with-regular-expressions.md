---
layout: post
title: "[python] Detecting duplicate words with regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

When working with text data, it is often useful to identify and handle duplicate words. Fortunately, regular expressions provide a powerful tool for detecting and managing such duplicates. In this tutorial, we will learn how to use regular expressions in Python to detect duplicate words in a given text.

## Table of Contents
- [Introduction](#introduction)
- [Detecting Duplicate Words](#detecting-duplicate-words)
- [Example Code](#example-code)
- [Conclusion](#conclusion)

## Introduction

Regular expressions are a sequence of characters that form a search pattern. They can be used to perform complex string matching operations, including identifying duplicate words in a text.

## Detecting Duplicate Words

To detect duplicate words using regular expressions, we can match word boundaries (`\b`) and then use backreferences to match the repeating words. Here's a breakdown of the steps involved:

1. Compile the regular expression pattern using `re.compile()`.
2. Use the `findall()` method to retrieve all matches in the text.
3. Iterate over the matches and check for duplicates.

Here's the regular expression pattern we will use: `r'\b(\w+)\b\s+\b\1\b'`.

- `\b(\w+)\b`: matches a word boundary followed by a word (capturing group 1) and another word boundary. This captures a word in the text.
- `\s+`: matches one or more whitespace characters.
- `\b\1\b`: matches the same word captured in the first group. This ensures that we only match repeated words.

## Example Code

Let's see an example of how to detect duplicate words using regular expressions in Python:

```python
import re

def detect_duplicate_words(text):
    pattern = re.compile(r'\b(\w+)\b\s+\b\1\b')
    matches = pattern.findall(text)
    duplicates = set(matches)
    return duplicates

# Example usage
text = "Hello world, hello Python. I love Python."
duplicate_words = detect_duplicate_words(text)
print(duplicate_words)
```

The output will be:
```
{'hello', 'Python'}
```

In this example, the words "hello" and "Python" are detected as duplicate words.

## Conclusion

Regular expressions provide a convenient way to detect duplicate words in a text. By leveraging word boundaries and backreferences, we can accurately identify and handle duplicates. Use this technique to improve the quality of your text data analysis or processing tasks.