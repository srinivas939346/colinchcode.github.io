---
layout: post
title: "[python] Extracting email addresses with regular expressions"
description: " "
date: 2023-09-29
tags: [python]
comments: true
share: true
---

In this tutorial, we will explore how to extract email addresses from a string using regular expressions in Python. Regular expressions are a powerful tool for pattern matching and can be used to easily extract email addresses from a given text.

## Prerequisites

Make sure you have Python installed on your system. If you haven't installed it yet, you can download it from the official Python website.

## Steps to Extract Email Addresses

1. Import the `re` module, which provides functions and methods to work with regular expressions.
   
   ```python
   import re
   ```

2. Define a regular expression pattern for matching email addresses. The pattern we'll use is `(\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}\b)`. Let's break it down:
   
   - `(\b[A-Za-z0-9._%+-]+)` matches the username part of the email address, which can contain letters, numbers, dots, underscores, plus and minus characters. The `\b` ensures that the username is matched as a whole word.
   - `@[A-Za-z0-9.-]+\.[A-Za-z]{2,}` matches the domain part of the email address, which includes the `@` symbol, followed by letters, numbers, dots, and dashes. The final part (`\.[A-Za-z]{2,}`) matches the top-level domain, such as `.com`, `.edu`, or `.org`.
   - The entire pattern is wrapped in parentheses to capture the matched email address.

3. Use the `re.findall()` function to find all occurrences of the email addresses in the given string. Pass the pattern and the input string as arguments to the function. The function returns a list of all matches found.
   
   ```python
   text = "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Email addresses can be extracted using regex. Here are a few examples: john.doe@example.com, jane_smith@domain.co.uk, info@example-email.com."
   email_pattern = re.compile(r'(\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}\b)')
   email_addresses = re.findall(email_pattern, text)
   ```

4. Iterate over the list of extracted email addresses and print each one.
   
   ```python
   for email in email_addresses:
       print(email)
   ```

## Conclusion

By using regular expressions, you can easily extract email addresses from a given text. The `re` module in Python provides powerful functions to work with regular expressions. Remember to validate the extracted email addresses as per your application's requirements.

Keep in mind that while the provided regular expression works well for most cases, there may be edge cases that it doesn't capture. Adjust the pattern as needed for your specific use case.