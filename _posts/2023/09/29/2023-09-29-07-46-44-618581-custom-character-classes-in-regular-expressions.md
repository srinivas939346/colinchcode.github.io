---
layout: post
title: "[python] Custom character classes in regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

Regular expressions are powerful tools for pattern matching and text manipulation. In Python, regular expressions are supported through the `re` module. One of the key features of regular expressions is the ability to define custom character classes. 

## What are Character Classes?

A character class is a set of characters enclosed within square brackets `[ ]` in a regular expression. It allows you to match any one character from the set.

For example, the regular expression `[aeiou]` matches any lowercase vowel. Similarly, `[0-9]` matches any digit, and `[A-Za-z]` matches any uppercase or lowercase letter.

## Custom Character Classes

Custom character classes allow you to define your own sets of characters. You can include or exclude specific characters as per your requirements.

To create a custom character class, you simply list the characters inside the square brackets. For example, to match either a digit or a letter, you can use `[0-9a-zA-Z]`. This will match any digit from 0 to 9, or any letter from a to z (both lowercase and uppercase).

### Negation

You can negate a character class by placing a caret `^` at the beginning. For example, `[^0-9]` matches any character that is not a digit. 

### Shorthand Character Classes

There are also shorthand character classes that provide a convenient way to match commonly used sets of characters. Some of the commonly used shorthand character classes include:

- `\d`: Matches any digit.
- `\D`: Matches any non-digit character.
- `\w`: Matches any alphanumeric character (letters, digits, and underscores).
- `\W`: Matches any non-alphanumeric character.
- `\s`: Matches any whitespace character (space, tab, newline).
- `\S`: Matches any non-whitespace character.

## Example Usage

Let's say we want to validate a password. We can use regular expressions with custom character classes to define the password requirements.

```python
import re

def validate_password(password):
    pattern = r"^[A-Za-z0-9@#$%]{8,}$"
    if re.match(pattern, password):
        return True
    return False

password1 = "Password123"  # Valid password
password2 = "P@ss"        # Invalid password

print(validate_password(password1))  # Output: True
print(validate_password(password2))  # Output: False
```

In the example above, `^[A-Za-z0-9@#$%]{8,}$` is the regular expression pattern. It requires the password to be at least 8 characters long and can only include uppercase letters, lowercase letters, digits, or the special characters @, #, $, and %. 

The `re.match()` function is used to check if the password matches the pattern.

## Conclusion

Custom character classes in regular expressions allow you to define your own sets of characters for pattern matching. They provide great flexibility when it comes to filtering and manipulating text. By mastering regular expressions and custom character classes, you can become more proficient in text processing and data extraction tasks.