---
layout: post
title: "[python] Replacing with regular expressions in Python"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

Regular expressions are powerful tools for pattern matching and text manipulation in Python. They provide a concise and efficient way to search, extract, and replace text based on specific patterns. In this tutorial, we will focus on how to use regular expressions to perform string replacements in Python.

## The `re` Module

Python provides the `re` module, which includes various functions and methods for working with regular expressions. To perform string replacements using regular expressions, we will primarily work with the `re.sub()` function.

## Syntax of `re.sub()`

The `re.sub()` function has the following syntax:

```python
re.sub(pattern, replacement, string, count=0, flags=0)
```

- `pattern`: The regular expression pattern to search for.
- `replacement`: The replacement string to be used.
- `string`: The input string on which the replacement is to be performed.
- `count` (optional): The maximum number of replacements to perform. Default is all occurrences.
- `flags` (optional): Additional flags for modifying the behavior of the regular expression matching. Common flags include `re.IGNORECASE`, `re.MULTILINE`, etc.

## Examples

Let's dive into some examples to see how we can use regular expressions to replace text in Python:

### Example 1: Simple Replacement

```python
import re

# Replace all occurrences of a word
text = "This is a sample text with some sample words."
replaced_text = re.sub(r'sample', 'modified', text)
print(replaced_text)
```

Output:
```
This is a modified text with some modified words.
```

In the above example, we replace all occurrences of the word "sample" with the word "modified" using `re.sub()`. Notice the use of the `r` prefix before the pattern to indicate it as a raw string.

### Example 2: Case Insensitive Replacement

```python
import re

# Replace a word case-insensitively
text = "This is a sample text with some Sample words."
replaced_text = re.sub(r'sample', 'modified', text, flags=re.IGNORECASE)
print(replaced_text)
```

Output:
```
This is a modified text with some modified words.
```

In this example, we use the `re.IGNORECASE` flag to perform a case-insensitive replacement. The word "Sample" is also replaced with "modified" alongside "sample".

### Example 3: Using a Function for Replacement

```python
import re

# Replace with a custom function
text = "The quick brown fox jumps over the lazy dog."
replaced_text = re.sub(r'\b\w{4,}\b', lambda x: x.group().upper(), text)
print(replaced_text)
```

Output:
```
The QUICK BROWN FOX JUMPS OVER THE LAZY DOG.
```

In this example, we replace words with four or more letters using a custom function. The `lambda x: x.group().upper()` function is called for each match found, and it returns the uppercase version of the match.

## Conclusion

Regular expressions offer a versatile and powerful way to replace text in Python. By using the `re` module's `sub()` function, we can easily perform string replacements based on specific patterns. Experiment with different regular expressions and their replacement patterns to master the art of text manipulation in Python.