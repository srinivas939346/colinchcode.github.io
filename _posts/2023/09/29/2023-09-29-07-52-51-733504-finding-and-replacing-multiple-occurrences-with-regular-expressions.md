---
layout: post
title: "[python] Finding and replacing multiple occurrences with regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

Regular expressions (regex) are a powerful tool for searching and manipulating strings in Python. They allow you to find and replace specific patterns or characters within a string.

In this tutorial, we will explore how to use regular expressions to find and replace multiple occurrences of a pattern in a string. We will be using the `re` module in Python, which provides support for regular expressions.

### Table of Contents
1. [Finding Multiple Occurrences](#finding-multiple-occurrences)
2. [Replacing Multiple Occurrences](#replacing-multiple-occurrences)
3. [Example Code](#example-code)
4. [Conclusion](#conclusion)

### Finding Multiple Occurrences
To find multiple occurrences of a pattern in a string, we can use the `re.findall()` function. This function returns a list of all non-overlapping matches as strings.

Here is an example that demonstrates how to find all occurrences of the word "apple" in a given string:

```python
import re

text = "I have an apple, and she has an apple too. We both love apples."
pattern = r"apple"

matches = re.findall(pattern, text)
print(matches)
```

Output:
```
['apple', 'apple', 'apple']
```

In the above code, we import the `re` module and define our string to search (`text`) and the pattern we want to find (`pattern`). The `r` before the pattern string is used to indicate that it's a raw string.

The `re.findall(pattern, text)` function then returns a list of all occurrences of the pattern within the given text.

### Replacing Multiple Occurrences
To replace multiple occurrences of a pattern in a string, we can use the `re.sub()` function. This function replaces all occurrences of a pattern with a specified replacement string.

Here is an example that demonstrates how to replace all occurrences of the word "apple" with "banana" in a given string:

```python
import re

text = "I have an apple, and she has an apple too. We both love apples."
pattern = r"apple"
replacement = "banana"

new_text = re.sub(pattern, replacement, text)
print(new_text)
```

Output:
```
I have an banana, and she has an banana too. We both love bananas.
```

In the above code, we define our string to search (`text`), the pattern we want to replace (`pattern`), and the replacement string (`replacement`).

The `re.sub(pattern, replacement, text)` function then replaces all occurrences of the pattern with the specified replacement string, and returns the modified string.

### Example Code

You can run the above code examples directly in Python to see the output.

Remember to import the `re` module before using regular expressions.

### Conclusion
Regular expressions provide a powerful and flexible way to search for and manipulate patterns in strings in Python. By using the `re.findall()` and `re.sub()` functions, you can easily find and replace multiple occurrences of a pattern within a string.

Experiment with different patterns and replacements to match the specific requirements of your project. Regular expressions can be complex, but with practice, you'll become proficient in using them to perform advanced string operations.