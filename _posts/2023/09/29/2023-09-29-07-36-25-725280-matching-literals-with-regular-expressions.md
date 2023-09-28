---
layout: post
title: "[python] Matching literals with regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

Regular expressions are powerful tools for pattern matching and text manipulation in Python. They allow you to find and manipulate specific patterns within strings. In this article, we will focus on using regular expressions to match literal strings.

## What are Literal Strings?

Literal strings are sequences of characters that are matched exactly as they are presented. For example, `"hello"` is a literal string that matches the characters "hello" in a given input text.

## Using Regular Expressions for Literal Matching

To match literal strings using regular expressions in Python, you can use the `re` module. Here is an example:

```python
import re

text = "The quick brown fox jumps over the lazy dog"
pattern = r"brown"

matches = re.findall(pattern, text)
print(matches)
```

In this example, we import the `re` module and define our text as `"The quick brown fox jumps over the lazy dog"`. We then define our pattern as `"brown"` and use the `re.findall()` function to find all occurrences of the pattern in the text. The `findall()` function returns a list of all matches.

The output of the above code will be:

```
['brown']
```

This tells us that the literal string `"brown"` was found in the input text.

## Escaping Special Characters

Keep in mind that some characters have special meanings in regular expressions. If you want to match these characters literally, you need to escape them using a backslash (`\`). Here are some examples:

```python
import re

text = "The quick brown fox jumps over the lazy dog"
pattern = r"\bthe\b"  # match the word "the" as a whole word, not as part of another word

matches = re.findall(pattern, text, re.IGNORECASE) # Use re.IGNORECASE for case-insensitive matching
print(matches)
```

In this example, we want to find occurrences of the word "the" as a whole word, not as part of another word. We use the word boundary assertions `\b` and escape the word "the" using `\`. The `re.IGNORECASE` flag is used to perform case-insensitive matching.

The output of the above code will be:

```
['The', 'the']
```

The regular expression matches both the upper case and lower case occurrences of the word "the" as whole words.

## Conclusion

Regular expressions provide a powerful way to match literal strings in Python. By using the `re` module and incorporating proper escaping of special characters, you can easily find and manipulate specific patterns within strings. This can be useful in various scenarios such as data validation, text preprocessing, or extracting specific information from text.