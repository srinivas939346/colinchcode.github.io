---
layout: post
title: "[python] Use of horizontal alignment in PEP 8 code"
description: " "
date: 2023-10-17
tags: [python]
comments: true
share: true
---

One common area where horizontal alignment is used in Python code is when defining variables with multiple assignments. For example:

```python
x = 10
y = 20
z = 30
```

In this case, the variables `x`, `y`, and `z` are aligned vertically to improve readability and make it easier to see that they are all assigned values.

However, PEP 8 advises against using horizontal alignment for long statements or lists of assignments. Instead, it recommends using a hanging indentation. Here's an example:

```python
long_variable_name = some_long_function_call(argument_1, argument_2,
                                             argument_3, argument_4)
```

In this example, the arguments are aligned with a hanging indent, meaning they are all vertically aligned after the opening parenthesis. This style is preferred over horizontal alignment for long or complex statements.

Overall, while horizontal alignment can be used in certain cases for improved readability, it's important to follow the guidelines in PEP 8 and prioritize code consistency and clarity.