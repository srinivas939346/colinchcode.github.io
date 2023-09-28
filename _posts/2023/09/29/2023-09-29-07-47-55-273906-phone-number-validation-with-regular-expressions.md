---
layout: post
title: "[python] Phone number validation with regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to validate phone numbers using regular expressions in Python. Regular expressions (regex) provide a powerful way to search, match, and validate text patterns.

## Why Use Regular Expressions?

Phone numbers can come in various formats, including different country codes, area codes, and number lengths. Validating phone numbers manually can be complex and error-prone. Regular expressions can simplify this process by defining a pattern to match against.

## The Regular Expression Pattern

Let's start by defining a regular expression pattern for validating phone numbers. In this example, we will assume a basic pattern where the phone number consists of 10 digits:

```python
import re

pattern = r"^\d{10}$"
```

Here, `r"^\d{10}$"` is the regular expression pattern. It consists of the following components:
- `^` - Matches the start of the string.
- `\d` - Matches any digit.
- `{10}` - Specifies that the previous element (digit) should occur exactly 10 times.
- `$` - Matches the end of the string.

## Using the Regular Expression

To validate a phone number using the regular expression pattern, we can use the `re` module in Python. Here's an example function that validates a given phone number:

```python
def validate_phone_number(phone_number):
    pattern = r"^\d{10}$"
    return bool(re.match(pattern, phone_number))
```

In this code, `re.match(pattern, phone_number)` checks if the given phone number matches the pattern. It returns a match object if there is a match or `None` otherwise. The `bool()` function is used to convert the match object to a boolean value.

## Testing the Validation Function

Let's test our `validate_phone_number()` function with some example phone numbers:

```python
phone_numbers = [
    "1234567890",
    "9876543210",
    "5555555555",
    "12345678",
    "abcdefghij",
    "1234abcd89"
]

for number in phone_numbers:
    if validate_phone_number(number):
        print(f"{number} is a valid phone number.")
    else:
        print(f"{number} is not a valid phone number.")
```

Running this code will validate each phone number in the list and display whether it is valid or not.

## Conclusion

Regular expressions are a powerful tool for validating text patterns, including phone numbers. By defining a regular expression pattern and using the `re` module in Python, we can easily validate phone numbers. This can be particularly useful when building applications that require accurate and consistent phone number validation.