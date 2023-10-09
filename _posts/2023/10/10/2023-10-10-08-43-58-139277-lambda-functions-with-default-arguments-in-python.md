---
layout: post
title: "[python] Lambda functions with default arguments in Python"
description: " "
date: 2023-10-10
tags: [python]
comments: true
share: true
---

Lambda functions, also known as anonymous functions, are a concise way to define functions in Python. They are commonly used in situations where a small, one-time function is needed.

One feature of lambda functions in Python is that they can take default arguments. Default arguments are values that a function assumes if no argument value is given during a function call. This allows for more flexibility when using lambda functions.

Let's take a look at an example of a lambda function with default arguments in Python.

```python
multiply = lambda x, y=2: x * y

print(multiply(3, 4))  # Output: 12
print(multiply(5))     # Output: 10
```

In this example, we define a lambda function called `multiply` that takes two arguments `x` and `y`. The default value of `y` is set to 2. When we call the `multiply` function with both arguments, it multiplies `x` and `y` and returns the result. In the first `print` statement, we pass both arguments and get the output of 12. In the second `print` statement, we only pass the `x` argument and the default value of `y` is used, resulting in the output of 10.

Lambda functions with default arguments can be useful when you want to create a custom function that has some predefined values, but also allows for flexibility by accepting additional or different arguments. This can simplify your code and make it more concise.

However, it's important to note that lambda functions should only be used for simple, one-liner functions and not for complex logic or extensive computation. They are meant to be small and focused functions that can be used inline wherever they are needed.

In conclusion, lambda functions with default arguments are a powerful feature of Python that allow you to define simple, anonymous functions with predefined values. They can be a useful tool when you need to quickly define a function on the fly, without the need for a formal function definition.