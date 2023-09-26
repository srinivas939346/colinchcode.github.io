---
layout: post
title: "[python] What is the difference between dict() and {} to create a dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

In Python, dictionaries are used to store key-value pairs. There are two common ways to create a dictionary: using the built-in `dict()` function or using the curly braces `{}`. While both methods accomplish the same task, there are some differences between them.

### Method 1: Using `dict()`
This method utilizes the `dict()` constructor to create a dictionary. It allows you to pass an iterable object or keyword arguments to initialize the dictionary.

Here is an example code using `dict()` to create a dictionary:


```python
my_dict = dict([('key1', 1), ('key2', 2)])
print(my_dict)
```

Output:
```
{'key1': 1, 'key2': 2}
```

### Method 2: Using `{}` (Curly Braces)
This method is known as dictionary literals. You can directly define key-value pairs inside the curly braces to create a dictionary.

Here is an example code using `{}` to create a dictionary:


```python
my_dict = {'key1': 1, 'key2': 2}
print(my_dict)
```

Output:
```
{'key1': 1, 'key2': 2}
```

### Difference between `dict()` and `{}`

1. **Readability**: Using `{}` to create a dictionary is more concise and easier to read compared to `dict()`, especially when working with smaller dictionaries.

2. **Familiarity**: The use of `{}` is more common in Python and is considered a Pythonic way of creating dictionaries.

3. **Performance**: Creating dictionaries using `{}` is generally faster than using `dict()`. This is due to the fact that `{}` directly calls the dictionary constructor, while `dict()` is a function call that involves some additional overhead.

4. **Flexibility**: The `dict()` function allows you to pass an iterable object or keyword arguments to initialize the dictionary. This can be useful in certain scenarios where you need more flexibility in defining the dictionary.

It's important to note that both methods are interchangeable, and you can use either based on your personal preference or specific requirements. However, the use of `{}` is more common and recommended in most cases for its simplicity and performance advantage.

Remember to choose the method that best suits your needs and keeps your code maintainable and readable.