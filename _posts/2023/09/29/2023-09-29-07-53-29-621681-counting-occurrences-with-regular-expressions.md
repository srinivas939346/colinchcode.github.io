---
layout: post
title: "[python] Counting occurrences with regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

Regular expressions are a powerful tool in Python for pattern matching and searching within text. One common use case is counting the occurrences of a particular pattern in a given string.

Let's say we want to count the number of times the word "Python" appears in a text. We can accomplish this using the `re` module in Python.

```python
import re

text = "Python is a great programming language. I love Python!"
pattern = r"Python"

# Count occurrences of the word "Python" in the text
occurrences = len(re.findall(pattern, text))

print(f"The word 'Python' appears {occurrences} times.")
```

Output:
```
The word 'Python' appears 2 times.
```

In the above code, we import the `re` module to work with regular expressions. We define our text and the pattern we want to search for using the regular expression `r"Python"`. The `r` before the pattern string indicates that it is a raw string, which helps to avoid any unwanted escape characters.

We then use the `re.findall()` function to find all occurrences of the pattern in the text. This function returns a list of matching strings. Finally, we use the `len()` function to count the number of occurrences.

By using regular expressions, we can easily count the occurrences of a pattern in a text, making it a versatile tool for various text processing tasks.