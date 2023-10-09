---
layout: post
title: "[python] Using lambda functions with filter() function in Python"
description: " "
date: 2023-10-10
tags: [python]
comments: true
share: true
---

In Python, `lambda` functions are anonymous functions that can be defined with a single expression. They are commonly used in combination with other functions like `filter()` to create powerful and concise code.

The `filter()` function is used to filter out elements from a sequence based on a given condition. It takes in two arguments: a function and an iterable (such as a list, tuple, or set). The function is used to test each element of the iterable, and only the elements that pass the test are returned in the result.

## Syntax of filter() function

The syntax for using `filter()` function with lambda functions is as follows:

```python
filter(lambda arguments: expression, iterable)
```

## Example usage

Let's say we have a list of numbers and we want to filter out only the even numbers. We can achieve this using a lambda function with the `filter()` function.

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

even_numbers = list(filter(lambda x: x % 2 == 0, numbers))

print(even_numbers)
```

Output:
```
[2, 4, 6, 8, 10]
```

In the above example, the lambda function `lambda x: x % 2 == 0` checks if a number is even or not by performing the modulus operation `%` with 2. If the result is 0, it means the number is even and it passes the filter.

The `filter()` function applies this lambda function to each element of the `numbers` list and returns a new list with only the even numbers.

## Conclusion

Using lambda functions with the `filter()` function in Python provides a concise way to filter elements from a sequence based on a given condition. By combining these two functions, you can write code that is both efficient and easy to understand.