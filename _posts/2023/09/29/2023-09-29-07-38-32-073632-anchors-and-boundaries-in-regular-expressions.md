---
layout: post
title: "[python] Anchors and boundaries in regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

Regular expressions (regex) are a powerful tool for pattern matching and searching in text. Anchors and boundaries are essential regex features that allow you to specify where a match should occur within a string. In this blog post, we will explore the various anchor and boundary characters available in Python's regex module.

## 1. Start and End Anchors

The start anchor (`^`) and end anchor (`$`) are used to match patterns that appear at the beginning and end of a string, respectively. For example, consider the following regex:

```
^Hello
```

This will match any string that starts with "Hello". Similarly, the regex:

```
world$
```

Will match any string that ends with "world".

Here's some Python code to demonstrate:

```python
import re

string = "Hello, world!"

# Using start anchor
match = re.search("^Hello", string)
print(match)  # Output: <re.Match object; span=(0, 5), match='Hello'>

# Using end anchor
match = re.search("world$", string)
print(match)  # Output: <re.Match object; span=(7, 12), match='world'>
```

## 2. Word Boundaries

Word boundaries (`\b`) can be used to match on the boundaries between word and non-word characters. For example, the regex:

```
\bcode\b
```

Will match the word "code" if it appears as a complete word, but not if it's a part of a longer word.

Here's some Python code to illustrate this:

```python
import re

string = "Learn to code with Python"

# Matching word "code"
match = re.search(r'\bcode\b', string)
print(match)  # Output: <re.Match object; span=(10, 14), match='code'>

# Non-word boundary example
match = re.search(r'\bpy\B', string)
print(match)  # Output: None
```

## 3. Line Anchors

Line anchors (`^` and `$` with the `re.MULTILINE` flag) are used to match patterns at the start and end of each line within a multiline string. Here's an example:

```python
import re

string = """Hello
World
Goodbye"""

# Matching at line start
matches = re.findall("^H", string, flags=re.MULTILINE)
print(matches)  # Output: ['H']

# Matching at line end
matches = re.findall("d$", string, flags=re.MULTILINE)
print(matches)  # Output: ['d']
```

In this example, we use the `re.MULTILINE` flag to enable multiline matching.

## Conclusion

Anchors and boundaries provide useful tools for specifying where matches should occur within a string. Understanding how to use them will empower you to write more precise regular expressions. Make sure to explore the official Python `re` module documentation for more details on these features and additional regex options.