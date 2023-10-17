---
layout: post
title: "[python] Use of inline comments and indentation in PEP 8"
description: " "
date: 2023-10-17
tags: [python]
comments: true
share: true
---

When writing Python code, following the guidelines set by PEP 8 is highly recommended. PEP 8 is the official style guide for Python code, and it helps ensure consistency and readability across different Python projects.

Inline comments and proper indentation are two important aspects of writing clean and readable code. Let's take a closer look at how PEP 8 suggests using inline comments and indentation.

## Inline Comments

Inline comments are useful for adding brief explanations or clarifications within your code. They should be used sparingly and should not state the obvious or duplicate the code. PEP 8 suggests following these guidelines for using inline comments:

1. **Keep them short**: Inline comments should be concise and to the point. Avoid writing lengthy explanations within your code.
2. **Start with a capital letter**: If your inline comment is a complete sentence, it should start with a capital letter.
3. **Separate comments from the code by at least two spaces**: This makes it easier to distinguish the code from the comments.
4. **Use proper punctuation**: Use proper punctuation at the end of your comment if it is a complete sentence.

Here's an example of using inline comments according to PEP 8:

```python
# Calculate the sum of two numbers
sum = number1 + number2

# Check if the sum is greater than 10
if sum > 10:
    print("Sum is greater than 10")
```

## Indentation

Proper indentation plays a crucial role in making your code readable and understandable. PEP 8 suggests the use of four spaces (not tabs) for indentation. Here are some guidelines for indentation according to PEP 8:

1. **Use four spaces for each level of indentation**: Avoid using tabs or a different number of spaces for indentation.
2. **Align continuation lines with the opening parenthesis or bracket**: If a statement needs to be continued in the next line, align it with the opening parenthesis or bracket of the previous line.

Here's an example of using proper indentation according to PEP 8:

```python
def calculate_sum(number1, number2):
    # Calculate the sum
    sum = number1 + number2

    # Print the sum
    print("Sum:", sum)

    if sum > 10:
        # Sum is greater than 10
        print("Sum is greater than 10")
```

Following these guidelines for inline comments and indentation will make your Python code more readable and consistent. It's always a good practice to stick to the standards set by PEP 8 for better collaboration and maintainability of your code.

References:
- [PEP 8 - Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/)
- [PEP 8 - Comments](https://www.python.org/dev/peps/pep-0008/#comments)
- [PEP 8 - Indentation](https://www.python.org/dev/peps/pep-0008/#indentation)