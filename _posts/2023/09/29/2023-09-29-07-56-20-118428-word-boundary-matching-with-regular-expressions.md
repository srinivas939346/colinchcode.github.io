---
layout: post
title: "[python] Word boundary matching with regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

To match word boundaries in Python regular expressions, you can use the special metacharacter `\b`. The `\b` represents a word boundary, which can be the start or end of a word. Here's an example:

```python
import re

text = "Hello, this is a sample text with some words."

# Match all words that start with 's'
pattern = r"\bs\w+"
matches = re.findall(pattern, text)
print(matches)  # Output: ['sample', 'some']

# Match all words that end with 's'
pattern = r"\w+s\b"
matches = re.findall(pattern, text)
print(matches)  # Output: ['this', 'is']

# Match all words that contain 'e' as a whole word
pattern = r"\b\w*e\w*\b"
matches = re.findall(pattern, text)
print(matches)  # Output: ['Hello', 'text', 'some']
```

In the example above, we use the `re.findall()` function from the `re` module to find all matching words in the `text` string based on the specified regular expression patterns. The patterns `\bs\w+`, `\w+s\b`, and `\b\w*e\w*\b` correspond to words starting with 's', words ending with 's', and words containing 'e' as a whole word, respectively.

Note that the use of word boundaries ensures that the regular expression matches complete words instead of partial matches within longer words. This is particularly useful when dealing with natural language text where only specific words are of interest.

By leveraging regular expressions and word boundaries, you can easily perform more complex word matching operations in Python, making it a versatile solution for various text processing tasks.