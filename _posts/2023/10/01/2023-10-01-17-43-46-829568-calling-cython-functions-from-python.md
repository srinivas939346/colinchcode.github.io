---
layout: post
title: "[python] Calling Cython functions from Python"
description: " "
date: 2023-10-01
tags: [python]
comments: true
share: true
---

Cython is a programming language that is a superset of Python. It allows you to write Python code that gets translated to C code, which can then be compiled to create highly efficient and fast modules.

In this tutorial, we will explore how to call Cython functions from Python.

## Prerequisites

Before we begin, make sure you have the following installed:

- Python (version 3 or above)
- Cython

## Step 1: Write Cython code

Create a new file with a `.pyx` extension, for example, `my_cython_module.pyx`. Inside this file, you can write pure Python code or use the Cython syntax to write optimized code.

```python
# my_cython_module.pyx

def my_cython_function(x):
    y = x * 2
    return y
```

## Step 2: Create a setup script

To compile the Cython code into a Python module, you need to create a `setup.py` script. This script contains instructions for building the module using Cython.

Create a new file named `setup.py` and add the following code:

```python
# setup.py

from distutils.core import setup
from Cython.Build import cythonize

setup(
    ext_modules=cythonize("my_cython_module.pyx")
)
```

## Step 3: Build the module

In your terminal or command prompt, navigate to the directory containing `setup.py` and run the following command:

```shell
python setup.py build_ext --inplace
```

This will build the Cython module and create a file with a `.so` (shared object) extension.

## Step 4: Import and use the module in Python

Now that you have built the Cython module, you can import it into your Python code and use the functions defined in it.

```python
import my_cython_module

result = my_cython_module.my_cython_function(5)
print(result)  # Output: 10
```

## Conclusion

Using Cython, you can write high-performance modules by leveraging the benefits of both Python and C. It provides an easy way to optimize your code and achieve faster execution times.

By following the steps outlined in this tutorial, you should now be able to call Cython functions from Python and harness the power of C in your Python projects.