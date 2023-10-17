---
layout: post
title: "[python] Guidelines for imported module and package names in PEP 8"
description: " "
date: 2023-10-17
tags: [python]
comments: true
share: true
---

When writing Python code, it's important to follow the guidelines set forth in [PEP 8](https://www.python.org/dev/peps/pep-0008/). This includes how we name the modules and packages we import in our code. Let's take a look at the guidelines for imported module and package names.

## Module Names

Module names should be short, lowercase, and descriptive. It's important to choose names that are understandable and meaningful to others who read our code. Avoid using abbreviations or acronyms unless they are widely known and accepted. Here are a few examples of well-named modules:

```python
import math
import requests
import datetime
```

## Package Names

Package names should follow the same rules as module names, but they can also use underscores if it improves readability. Package names should be all lowercase and avoid using any special characters or punctuation. For example:

```python
import my_package
import data_analysis
```

## Importing Multiple Modules

When importing multiple modules from the same package, it's recommended to import them individually and not use the wildcard import ("*"). This makes it clearer which specific modules are being imported and used in the code. For example:

```python
from my_package import module1, module2
```

## Alias or Renaming Imports

Sometimes, names of imported modules or packages can be too long or clash with other names in our code. In such cases, it's acceptable to use an alias or rename the import using the `as` keyword. However, it's important to choose alias names that are still easy to understand. Here's an example:

```python
import matplotlib.pyplot as plt
import pandas as pd
```

## Nested Packages

When importing modules from nested packages, use the dot notation to maintain clarity and readability. For example:

```python
from my_package.subpackage import module1, module2
```

Following these guidelines for imported module and package names helps ensure that our code is clean, consistent, and easy to understand for ourselves and others. By adhering to the conventions laid out in PEP 8, we contribute to the overall maintainability of Python codebases.