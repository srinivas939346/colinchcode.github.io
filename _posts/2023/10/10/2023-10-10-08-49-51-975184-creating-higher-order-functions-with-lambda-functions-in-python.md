---
layout: post
title: "[python] Creating higher-order functions with lambda functions in Python"
description: " "
date: 2023-10-10
tags: [python]
comments: true
share: true
---

Python is a versatile and powerful programming language that allows you to work with functions as first-class citizens. This means that you can pass functions as arguments to other functions, return functions from functions, and even create functions on the fly. One way to create functions on the fly is by using lambda functions.

## Lambda functions in Python

Lambda functions, also known as anonymous functions, are small and anonymous functions that can be defined without a name. They are commonly used to create ad-hoc functions that are used only once and don't require a full function definition.

The syntax for creating a lambda function is as follows:

```python
lambda arguments: expression
```

The `arguments` are the input variables of the lambda function, and the `expression` is the operation that will be performed on the arguments.

## Higher-order functions

In functional programming, a higher-order function is a function that can take other functions as arguments or return a function as its result. A higher-order function allows you to abstract over actions, rather than just values. This abstraction provides a powerful way to express concepts and manipulate behavior in your programs.

Let's see an example of a higher-order function that takes a lambda function as an argument:

```python
def apply_operation(x, y, operation):
    return operation(x, y)
```

In this example, the `apply_operation` function takes three arguments: `x`, `y`, and `operation`. The `operation` argument is a lambda function that performs some kind of operation on `x` and `y`. The `apply_operation` function then calls the `operation` function with `x` and `y` as its arguments and returns the result.

## Example usage

Here's an example usage of the `apply_operation` function with a lambda function:

```python
addition = lambda x, y: x + y
result = apply_operation(2, 3, addition)
print(result)  # Output: 5
```

In this example, we create a lambda function called `addition` that takes two arguments `x` and `y` and returns their sum. We then pass this lambda function as the `operation` argument to the `apply_operation` function along with the values `2` and `3`. The `apply_operation` function calls the `addition` function with `2` and `3` and returns the result, which is then printed. The output is `5`.

## Conclusion

Lambda functions in Python allow you to create small ad-hoc functions on the fly without the need for a full function definition. Combined with higher-order functions, you can achieve powerful abstractions and manipulate behavior in your code. By leveraging lambda functions and higher-order functions, you can write more concise and expressive code in Python.