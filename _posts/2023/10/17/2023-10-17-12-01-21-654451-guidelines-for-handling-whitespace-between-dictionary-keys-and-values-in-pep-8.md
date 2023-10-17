---
layout: post
title: "[python] Guidelines for handling whitespace between dictionary keys and values in PEP 8"
description: " "
date: 2023-10-17
tags: [python]
comments: true
share: true
---

When working with dictionaries in Python, it is essential to follow certain guidelines to maintain code readability and consistency. The Python Enhancement Proposal (PEP) 8 provides the standard style guide for Python code, including suggestions on handling whitespace in dictionaries.

Here are the guidelines for handling whitespace between dictionary keys and values in PEP 8:

### 1. Space Around Colons

In a dictionary, a colon is used to separate keys from their corresponding values. According to PEP 8, there should always be **no space before the colon** and a **single space after the colon**.

Example:

```python
# Good
my_dict = {'key': 'value'}

# Bad
my_dict = {'key' :'value'}
my_dict = {'key':'value'}
```

### 2. Spaces Between Key-Value Pairs

When defining multiple key-value pairs in a dictionary, there should be a **single space before and after the comma** separating each pair. 

Example:

```python
# Good
my_dict = {'key1': 'value1', 'key2': 'value2'}

# Bad
my_dict = {'key1':'value1', 'key2':'value2'}
my_dict = {'key1': 'value1','key2': 'value2'}
```

### 3. Indentation of Dictionary Pairs

If a dictionary has multiple key-value pairs, each pair should be **indented on a new line** with respect to the opening and closing braces. The closing brace should align horizontally with the opening brace.

Example:

```python
# Good
my_dict = {
    'key1': 'value1',
    'key2': 'value2'
}

# Bad
my_dict = {'key1': 'value1',
           'key2': 'value2'}
```

Following these guidelines ensures that your code is clean, readable, and consistent with PEP 8 recommendations. Consistency across different projects and codebases makes collaboration and maintenance easier.

For further information, you can refer to the [PEP 8 documentation](https://www.python.org/dev/peps/pep-0008/), which provides detailed guidelines on Python code styling and best practices.

Remember that adhering to these guidelines improves code readability and helps maintain a consistent coding style, making your code more accessible and understandable for others.