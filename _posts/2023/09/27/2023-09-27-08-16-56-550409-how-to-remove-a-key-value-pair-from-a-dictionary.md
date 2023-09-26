---
layout: post
title: "[python] How to remove a key-value pair from a dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

In Python, a dictionary is a collection of key-value pairs, where each key is unique. Sometimes, we may need to remove a specific key-value pair from the dictionary. In this article, we will explore different methods to accomplish this task.

## Method 1: Using the `del` keyword

The simplest way to remove a key-value pair from a dictionary is by using the `del` keyword. We can specify the key that we want to delete, and Python will remove the corresponding key-value pair from the dictionary.

Here's an example:

```python
my_dict = {'name': 'John', 'age': 25, 'city': 'New York'}
del my_dict['age']
print(my_dict)
```

Output:
```
{'name': 'John', 'city': 'New York'}
```

In the example above, we have a dictionary `my_dict` with three key-value pairs. By using `del my_dict['age']`, we remove the key-value pair with the key `'age'` from the dictionary.

## Method 2: Using the `pop()` method

Another way to remove a key-value pair from a dictionary is by using the `pop()` method. The `pop()` method takes the key as an argument and returns the corresponding value. It also removes the key-value pair from the dictionary.

Here's an example:

```python
my_dict = {'name': 'John', 'age': 25, 'city': 'New York'}
removed_value = my_dict.pop('age')
print(my_dict)
print(removed_value)
```

Output:
```
{'name': 'John', 'city': 'New York'}
25
```

In the example above, we use `my_dict.pop('age')` to remove the key-value pair with the key `'age'` from the dictionary. The returned value is assigned to the variable `removed_value`.

## Method 3: Using the `popitem()` method

If you want to remove a random key-value pair from the dictionary, you can use the `popitem()` method. The `popitem()` method removes and returns an arbitrary key-value pair as a tuple.

Here's an example:

```python
my_dict = {'name': 'John', 'age': 25, 'city': 'New York'}
removed_item = my_dict.popitem()
print(my_dict)
print(removed_item)
```

Output:
```
{'name': 'John', 'age': 25}
('city', 'New York')
```

In the example above, we use `my_dict.popitem()` to remove an arbitrary key-value pair from the dictionary. The removed key-value pair is assigned to the variable `removed_item` as a tuple.

## Conclusion

You can remove a key-value pair from a dictionary in Python using the `del` keyword, the `pop()` method, or the `popitem()` method. Choose the method that best suits your needs based on whether you want to specify the key or remove a random key-value pair.