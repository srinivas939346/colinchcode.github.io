---
layout: post
title: "[python] Email validation with regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

Email validation is a common task in web application development. It ensures that the email addresses provided by users are in the correct format. In this article, we will explore how to validate email addresses using regular expressions in Python.

## Regular Expressions

Regular expressions, also known as regex, are sequences of characters that define a search pattern. They are a powerful tool for pattern matching and string manipulation. In Python, regular expressions can be used with the `re` module.

## Email Validation Pattern

To validate email addresses, we need to define a pattern that matches the correct format of an email address. Although a full-fledged regex pattern for email validation can be complex, we can start with a simpler version that covers most common cases.

Here's an example pattern for email validation using regular expressions:

```
^[\w\.-]+@[\w\.-]+\.\w+$
```

Let's break down this pattern:

- `^` asserts the start of the string.
- `[\w\.-]+` matches one or more word characters (letters, digits, and underscores), dots, or dashes for the first part of the email address (before the at symbol).
- `@` matches the at symbol.
- `[\w\.-]+` matches one or more word characters, dots, or dashes for the domain name (after the at symbol).
- `\.` matches a literal dot (period).
- `\w+` matches one or more word characters for the top-level domain.
- `$` asserts the end of the string.

## Python Implementation

Now, let's see how we can implement email validation in Python using regular expressions.

```python
import re

def is_valid_email(email):
    pattern = r'^[\w\.-]+@[\w\.-]+\.\w+$'
    if re.match(pattern, email):
        return True
    return False
```

In the code above, we define a function `is_valid_email` that takes an email address as input. The function uses the `re.match` method to match the provided email against the defined regex pattern.

If the email matches the pattern, the function returns `True`, indicating a valid email address. Otherwise, it returns `False`.

## Testing the Validation Function

Let's test our `is_valid_email` function with some sample email addresses:

```python
print(is_valid_email("john.doe@example.com"))    # True
print(is_valid_email("jane!doe@example.com"))    # False
print(is_valid_email("invalid_email.com"))       # False
print(is_valid_email("john.doe@example"))        # False
```

By running the code above, we should see the following output:

```
True
False
False
False
```

The function correctly identifies valid and invalid email addresses based on the defined pattern.

## Conclusion

Using regular expressions, we can easily validate email addresses in Python. Although the provided pattern covers most common cases, email address validation can be more complex depending on your requirements. It's important to keep in mind that no email validation is perfect, and it's a best practice to combine regex validation with additional checks and verifications.