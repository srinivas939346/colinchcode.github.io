---
layout: post
title: "[python] Grouping in regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

Regular expressions are a powerful tool for pattern matching and string manipulation in programming. One of the key features of regular expressions is the ability to group certain parts of a pattern together. Grouping allows you to treat multiple characters as a single unit, which can help in creating more complex and flexible regular expression patterns.

In this blog post, we'll explore how grouping works in regular expressions and how it can be useful in various scenarios.

## Basic Grouping

The simplest form of grouping in regular expressions is to enclose a set of characters within parentheses `()`. For example, let's say we want to match either "cat" or "dog" followed by "s". We can define a pattern with grouping as `(cat|dog)s`, where `(cat|dog)` is a group:

```python
import re

pattern = "(cat|dog)s"
text = "cats and dogs are great companions"

matches = re.findall(pattern, text)

print(matches)  # Output: ['cat', 'dog']
```

In this example, the regular expression `(cat|dog)s` matches either "cat" or "dog" followed by "s". The `findall()` function returns all the matches found in the text.

## Capturing Groups

Groups not only allow us to treat multiple characters as a unit but also provide a way to extract specific parts of a match. These groups are called capturing groups, and they are assigned a number starting from 1 based on their position left to right.

Let's say we want to extract the words that follow "I love" in a sentence. We can define a pattern with a capturing group like this:

```python
import re

pattern = "I love (\w+)"
text = "I love coding, I love writing, and I love exploring."

matches = re.findall(pattern, text)

print(matches)  # Output: ['coding', 'writing', 'exploring']
```

In this example, the regular expression `I love (\w+)` captures one or more word characters after the phrase "I love". The `findall()` function returns all the captured values.

## Non-Capturing Groups

Sometimes, we may want to use grouping for logical purposes but don't need to capture the matched text. Non-capturing groups `(?:)` can come in handy in such situations.

For instance, let's say we want to match a pattern where a word is followed either by "ing" or "ed" but not capture the actual suffix:

```python
import re

pattern = r"\b\w+(?:ing|ed)\b"
text = "I am singing while he danced."

matches = re.findall(pattern, text)

print(matches)  # Output: ['singing', 'danced']
```

In this example, the regular expression `\b\w+(?:ing|ed)\b` matches one or more word characters followed by either "ing" or "ed" without capturing the matched suffix.

## Conclusion

Grouping in regular expressions allows you to treat multiple characters as a single unit and provides flexibility in creating more complex patterns. Capturing groups enable you to extract specific parts of a match, while non-capturing groups are useful for logical grouping without capturing the matched text. Understanding and utilizing grouping can significantly enhance your regular expression skills and make your pattern matching tasks more powerful and efficient.