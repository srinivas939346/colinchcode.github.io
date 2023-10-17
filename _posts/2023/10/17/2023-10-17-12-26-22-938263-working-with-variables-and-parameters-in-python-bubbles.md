---
layout: post
title: "[python] Working with variables and parameters in Python Bubbles."
description: " "
date: 2023-10-17
tags: [python]
comments: true
share: true
---

In Python, variables are used to store data values that can be accessed and manipulated by the program. Parameters, on the other hand, are special variables that are used to pass values into functions or methods.

Let's dive into Python Bubbles, a library specifically designed for bubble sorting algorithms, and explore how variables and parameters are used.

## Declaring Variables

In Python, variables are declared by assigning a value to them using the assignment operator `=`. Python is dynamically typed, so you don't need to explicitly declare the variable's data type.

```python
x = 10
name = "John"
pi = 3.14
```

In the above example, we declare three different variables - `x`, `name`, and `pi` - with different data types. The variables can be assigned new values later in the program.

## Function Parameters

Parameters in Python are used to pass values into functions or methods. They act as placeholders for the actual values that will be supplied when the function is called.

```python
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")
```

In the above code snippet, we define a function called `greet` that takes a single parameter `name`. When the function is called with the argument "Alice", it will print "Hello, Alice!".

## Using Variables and Parameters in Python Bubbles

Now let's explore how variables and parameters are used in the context of Python Bubbles.

```python
from bubbles import bubble_sort

# Example 1: Sorting a list of numbers
numbers = [5, 2, 8, 1, 9]
bubble_sort(numbers)
print(numbers)  # Output: [1, 2, 5, 8, 9]

# Example 2: Sorting a list of strings
names = ["Alice", "Bob", "Charlie"]
bubble_sort(names)
print(names)  # Output: ['Alice', 'Bob', 'Charlie']
```

In the above code, we import the `bubble_sort` function from the `bubbles` module. The function takes a list as a parameter and sorts it using the bubble sort algorithm.

In Example 1, we declare a variable `numbers` and assign it a list of numbers. We pass this variable as an argument to the `bubble_sort` function, which sorts the list in ascending order. After sorting, we print the sorted list.

In Example 2, we declare a variable `names` and assign it a list of strings. Similarly, we pass this variable as an argument to the `bubble_sort` function, which sorts the list in lexicographic order.

As you can see, variables and parameters play an important role in Python Bubbles for storing and manipulating data.

## Conclusion

In this blog post, we explored how variables and parameters are used in Python Bubbles. We learned how to declare variables, pass values as function parameters, and use them in the context of the bubble sort algorithm. Understanding variables and parameters is crucial for writing effective and efficient code in Python.

To learn more about Python Bubbles and other algorithms, check out the [official documentation](https://python-bubbles.readthedocs.io/).