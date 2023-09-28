---
layout: post
title: "[python] Alternation in regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

To understand how alternation works in regular expressions, consider a scenario where you want to match either "cat" or "dog" in a given text. You can use the following regex pattern:
```python
import re

text = "I have a cat and a dog."
pattern = r"cat|dog"

matches = re.findall(pattern, text)
print(matches)  # Output: ['cat', 'dog']
```

In this example, the regex pattern `cat|dog` will match either "cat" or "dog". When you use `re.findall()` with this pattern on the `text`, it will return a list of all matching occurrences in the text.

You can also use alternation to match more complex patterns. For instance, consider a scenario where you want to match either an email address or a phone number in a text. You can modify the regex pattern as follows:
```python
import re

text = "Contact me at john@example.com or call 123-456-7890."
pattern = r"\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}\b|\d{3}-\d{3}-\d{4}"

matches = re.findall(pattern, text)
print(matches)  # Output: ['john@example.com', '123-456-7890']
```

In this example, the regex pattern uses alternation to match either an email address or a phone number. The first alternative pattern `\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}\b` matches an email address, while the second alternative pattern `\d{3}-\d{3}-\d{4}` matches a phone number.

Alternation in regular expressions provides a flexible way to match multiple alternatives within a single pattern. By using the `|` operator, you can easily specify different options for matching different parts of the text. This enables you to write more concise and versatile regex patterns in Python.