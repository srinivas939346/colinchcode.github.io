---
layout: post
title: "[python] Mapping elements using lambda functions in Python"
description: " "
date: 2023-10-10
tags: [python]
comments: true
share: true
---

In Python, the `map()` function is used to apply a function to each element of an iterable and return the result as a new iterator. One common way to define the function to be applied is by using **lambda functions**.

## What is a Lambda Function?

A lambda function, also known as an **anonymous function**, is a small, one-line function that does not have a name. It is defined using the `lambda` keyword, followed by a list of arguments, a colon (`:`), and the expression to be evaluated.

```python
lambda arguments: expression
```

Lambda functions are convenient when you need to define a small function without explicitly naming it.

## Using Lambda Functions with `map()`

The `map()` function takes two arguments: the function to be applied and the iterable to be mapped. It applies the specified function to each element of the iterable and returns the results as a new iterator.

Here's an example that uses a lambda function to square each element in a list of numbers:

```python
numbers = [1, 2, 3, 4, 5]
squared_numbers = list(map(lambda x: x ** 2, numbers))
print(squared_numbers)
```

**Output:**
```
[1, 4, 9, 16, 25]
```

In the example above, we define a lambda function `lambda x: x ** 2` that squares each element `x`. We then use `map()` to apply this lambda function to each element in the `numbers` list. The result is a new list `squared_numbers` containing the squared values.

Lambda functions can also be used with multiple arguments and multiple iterables. Here's an example that calculates the sum of two lists element-wise:

```python
list1 = [1, 2, 3, 4]
list2 = [5, 6, 7, 8]
sum_list = list(map(lambda x, y: x + y, list1, list2))
print(sum_list)
```

**Output:**
```
[6, 8, 10, 12]
```

In the example above, we define a lambda function `lambda x, y: x + y` that adds each pair of elements `x` and `y`. We then use `map()` to apply this lambda function to corresponding elements of `list1` and `list2`. The result is a new list `sum_list` containing the sum of each pair.

## Conclusion

Lambda functions provide a concise way to define small functions without naming them explicitly. When combined with the `map()` function, lambda functions can be used to apply a function to each element of an iterable and return the results as a new iterator. This allows for flexible and efficient element-wise operations in Python.