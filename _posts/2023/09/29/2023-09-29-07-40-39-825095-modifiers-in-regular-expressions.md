---
layout: post
title: "[python] Modifiers in regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

Regular expressions are a powerful tool for pattern matching and string manipulation. They allow us to define complex search patterns and perform various operations on strings. In Python, regular expressions are built-in with the `re` module.

Modifiers, also known as flags or options, are used to add extra functionality to regular expressions. They can modify the behavior of the pattern matching process and give us more control over how the patterns are matched.

In Python, modifiers are represented by one or more characters that are added after the closing delimiter of the regular expression pattern. Let's explore some common modifiers and their usage.

## Case Insensitive Matching - `re.IGNORECASE` or `re.I`

By default, regular expressions in Python are case sensitive, so uppercase and lowercase letters are considered different. However, if we want to perform a case-insensitive search, we can use the `re.IGNORECASE` or `re.I` modifier. This allows the pattern to match regardless of the case of the letters.

Here's an example:

```python
import re

pattern = r"apple"
text = "I have an Apple"
match = re.search(pattern, text, re.IGNORECASE)

if match:
    print("Match found!")
else:
    print("No match found.")
```

Output:

```
Match found!
```

In the above example, the `re.IGNORECASE` modifier is passed as the third argument to the `re.search()` function. It ignores the case of the letters in the pattern and successfully finds a match.

## Multiline Matching - `re.MULTILINE` or `re.M`

By default, regular expressions treat a string as a single line, where `^` and `$` match the start and end of the entire string, respectively. However, if we want to apply these anchors on each line instead, we can use the `re.MULTILINE` or `re.M` modifier.

Here's an example:

```python
import re

pattern = r"^apple"
text = "apple\nbanana\ncherry"
match = re.findall(pattern, text, re.MULTILINE)

if match:
    print("Matches found!")
    for m in match:
        print(m)
else:
    print("No match found.")
```

Output:

```
Matches found!
apple
```

In the above example, the `re.MULTILINE` modifier is passed as the third argument to the `re.findall()` function. It applies the `^` anchor to each line and finds a match only at the beginning of the first line.

## Dot All - `re.DOTALL` or `re.S`

By default, the dot (`.`) metacharacter in regular expressions matches any character except a newline. However, if we want the dot to match any character including newlines, we can use the `re.DOTALL` or `re.S` modifier.

Here's an example:

```python
import re

pattern = r"apple.*cherry"
text = "apple\nbanana\ncherry"
match = re.search(pattern, text, re.DOTALL)

if match:
    print("Match found!")
    print(match.group())
else:
    print("No match found.")
```

Output:

```
Match found!
apple
banana
cherry
```

In the above example, the `re.DOTALL` modifier is passed as the third argument to the `re.search()` function. It allows the dot to match newlines, and we get a match that spans multiple lines.

These are just a few examples of modifiers in regular expressions. Python provides more modifiers that offer additional functionalities and control over the pattern matching process. You can refer to the [Python documentation](https://docs.python.org/3/library/re.html) for more information on regular expression modifiers and their usage.