---
layout: post
title: "[python] Scope of variables in lambda functions in Python"
description: " "
date: 2023-10-10
tags: [python]
comments: true
share: true
---

In Python, a lambda function is an anonymous function that can be defined in a single line without a name. One common question that arises when using lambda functions is about the scope of variables inside them.

## Global Variables

If a variable is defined outside the lambda function, it can be accessed and used inside the lambda function as well. Let's take a look at an example:

```python
x = 10

func = lambda y: x + y

print(func(5))  # Output: 15
```

In the above code, `x` is a global variable that is accessible inside the lambda function `func`.

## Local Variables

Lambda functions can also access and use local variables defined within their enclosing function. Here's an example:

```python
def outer_func():
    x = 10
    func = lambda y: x + y
    return func

inner_func = outer_func()
print(inner_func(5))  # Output: 15
```

In this case, the lambda function `func` has access to the variable `x` defined in `outer_func`. This is because the closure of the lambda function retains the reference to the variable `x` even after `outer_func` has finished executing.

## Modifying Variables

If you attempt to modify a variable defined outside the lambda function from within the lambda function, Python will consider it as a new local variable. Here's an example to illustrate this:

```python
x = 10
func = lambda: x + 5
print(func())  # Output: 15

x = 20
print(func())  # Output: 25
```

In the above code, the lambda function `func` does not modify the global variable `x`. Instead, it creates a new local variable `x` inside the function.

## Conclusion

In summary, lambda functions in Python have access to variables defined outside of them, including both global and local variables. However, modifying variables outside the lambda function will create a new local variable rather than modifying the original variable.