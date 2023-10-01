---
layout: post
title: "[python] Declaring variables in Cython"
description: " "
date: 2023-10-01
tags: [python]
comments: true
share: true
---

To declare variables in Cython, you can use the `cdef` keyword, followed by the type and name of the variable. Here's an example of declaring variables in Cython:

```python
cdef int my_integer
cdef float my_float
cdef char my_char
```

In this example, we declare three variables: `my_integer` of type `int`, `my_float` of type `float`, and `my_char` of type `char`.

You can also assign values to these variables at the time of declaration. Here's an example:

```python
cdef int my_integer = 10
cdef float my_float = 3.14
cdef char my_char = 'a'
```

In addition to the basic types like `int`, `float`, and `char`, Cython also supports other C types such as `double`, `long`, `short`, etc. You can declare variables of these types in the same way.

It's worth noting that when declaring variables with specific types in Cython, you gain the advantage of static typing, which can lead to better performance compared to dynamically typed code in regular Python. However, you need to ensure that the declared types are compatible with the operations you perform on the variables.

By using the `cdef` keyword to declare variables in Cython, you can enjoy the benefits of static typing and write high-performance code that is closer to C while still allowing Python-like syntax.