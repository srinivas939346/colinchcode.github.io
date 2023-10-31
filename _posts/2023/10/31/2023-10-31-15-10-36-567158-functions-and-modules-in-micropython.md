---
layout: post
title: "[python] Functions and modules in MicroPython"
description: " "
date: 2023-10-31
tags: [python]
comments: true
share: true
---

MicroPython is a lightweight implementation of the Python programming language that is optimized for microcontrollers and other constrained environments. In MicroPython, you can use functions and modules to organize and reuse your code effectively. In this article, we will explore how to create and use functions and modules in MicroPython.

### Functions

Functions are blocks of reusable code that perform a specific task. They help in modularizing your code and making it more readable and organized. Here's an example of defining and calling a function in MicroPython:

```python
# Define a function
def greet(name):
    print("Hello, " + name + "!")

# Call the function
greet("MicroPython")
```

In the above code, we define a function called `greet` that takes one argument `name`. It prints a greeting message with the provided name. We then call the function passing `"MicroPython"` as the argument.

You can also define functions with default arguments:

```python
# Define a function with default argument
def greet(name="World"):
    print("Hello, " + name + "!")

# Call the function
greet()  # Prints "Hello, World!"
greet("MicroPython")  # Prints "Hello, MicroPython!"
```

In this case, if no argument is provided while calling the function, it uses the default value `"World"`.

### Modules

Modules in MicroPython are separate files that contain functions, variables, and classes. They help in organizing your code into logical units and promote code reusability. To use functions defined in a module, you need to import the module into your code. Here's an example:

```python
# Define a module in a separate file named utils.py
# utils.py
def calculate_sum(a, b):
    return a + b

# main.py
import utils

result = utils.calculate_sum(3, 4)
print(result)  # Prints 7
```

In the above example, we have a module `utils.py` that contains a function `calculate_sum`. In `main.py`, we import the `utils` module and use the `calculate_sum` function to calculate the sum of two numbers.

You can also import specific functions or variables from a module:

```python
# main.py
from utils import calculate_sum

result = calculate_sum(3, 4)
print(result)  # Prints 7
```

In this case, we only import the `calculate_sum` function from the `utils` module.

### Conclusion

Functions and modules are essential concepts in MicroPython for organizing and reusing code. Functions help in modularizing your code and making it more readable, while modules allow you to separate code into logical units. By using functions and modules effectively, you can write cleaner and more maintainable MicroPython code.

References:
- [MicroPython official website](https://micropython.org/)
- [MicroPython documentation](https://docs.micropython.org/)