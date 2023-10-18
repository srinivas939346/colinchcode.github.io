---
layout: post
title: "[python] Iterable vs. iterator in Python generators"
description: " "
date: 2023-10-18
tags: [python]
comments: true
share: true
---

When working with Python generators, it's important to understand the concepts of iterables and iterators. These terms often come up when dealing with sequences or collections of data in Python. In this blog post, we will explore the differences between iterables and iterators, and how they relate to Python generators.

## Iterable

In Python, an iterable is an object that can be looped over. It is a general term used to describe any object that can return an iterator. Examples of iterables include lists, tuples, strings, and even generators.

Here's an example of an iterable list:
```python
my_list = [1, 2, 3, 4, 5]
```

## Iterator

An iterator, on the other hand, is an object that represents a stream of data. It is responsible for producing the next value in the sequence. Iterators have a special method called `__next__()` that returns the next item in the sequence. If there are no more items to return, it raises the `StopIteration` exception.

In Python, an iterator object must implement the `__iter__()` method, which returns itself. This allows the iterator to be looped over multiple times.

Here's an example of an iterator using a generator function:
```python
def my_generator():
    yield 1
    yield 2
    yield 3
    yield 4
    yield 5

my_iterator = my_generator()
```

`my_iterator` is an iterator object created by calling the generator function `my_generator()`. It will produce the next value in the sequence each time the `__next__()` method is called on it.

## Relationship Between Iterables and Iterators

Now that we understand the concepts of iterables and iterators, let's discuss their relationship. An iterable object, such as a list or a string, can be iterated over by creating an iterator from it. The iterator is then used to retrieve the items from the iterable one by one.

In Python, the `iter()` function is used to create an iterator from an iterable. It calls the iterable's `__iter__()` method, which returns the iterator object.

Here's an example of creating an iterator from an iterable:
```python
my_list = [1, 2, 3, 4, 5]
my_iterator = iter(my_list)
```

Once you have an iterator object, you can use it to retrieve the items one by one using the `__next__()` method.

```python
print(next(my_iterator))  # Output: 1
print(next(my_iterator))  # Output: 2
print(next(my_iterator))  # Output: 3
```

## Conclusion

In summary, iterables are objects that can be looped over, while iterators are objects that produce the next value in a sequence. Python generators act as both iterables and iterators. Understanding these concepts will help you make the most of Python's powerful generator functionality.

For more information about Python generators, you can refer to the [Python documentation](https://docs.python.org/3/tutorial/classes.html#generators).