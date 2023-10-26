---
layout: post
title: "[python] Type annotation in static typing"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Type annotations are done using the **`typing`** module, which provides different types and constructs for static typing. Let's take a look at some common use cases for type annotation in Python.

**1. Function Annotations:**

Function annotations allow you to specify the expected type of function arguments and return value. Here is an example:

```python
from typing import List

def calculate_sum(nums: List[int]) -> int:
    return sum(nums)
```

In this example, the argument `nums` is annotated as `List[int]`, indicating that it should be a list of integers. The return value is annotated as `int`, specifying that the function should return an integer. These annotations improve code readability and provide better understanding of the expected inputs and outputs of a function.

**2. Variable Annotations:**

You can also annotate variables with their expected types. Here is an example:

```python
from typing import Optional

name: str = "John"
age: int = 25
is_active: bool = True
email: Optional[str] = None
```

In this example, the variables `name`, `age`, and `is_active` are annotated with their respective types. The `email` variable is annotated as `Optional[str]`, indicating that it can either be a string or `None`. Annotating variables helps in self-documenting code and avoids type-related bugs.

**3. Class Annotations:**

Class variables and instance variables can also be annotated with their expected types. Here is an example:

```python
from typing import List

class Employee:
    emp_ids: List[int] = []
    name: str
    age: int
    
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age
```

In this example, the class variable `emp_ids` is annotated as `List[int]`, indicating that it should be a list of integers. The instance variables `name` and `age` are annotated with their respective types. Class annotations provide clear information about the expected types of variables at class and instance level.

Overall, type annotation in Python brings the benefits of static typing while still retaining the flexibility and dynamic nature of the language. It is recommended to use type annotations in conjunction with a static type checker like **`mypy`** to catch type-related errors during development.

References:
- [PEP 3107 -- Function Annotations](https://www.python.org/dev/peps/pep-3107/)
- [PEP 484 -- Type Hints](https://www.python.org/dev/peps/pep-0484/)
- [Python Typing](https://docs.python.org/3/library/typing.html)