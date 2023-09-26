---
layout: post
title: "[python] How to update a value in a nested dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

In Python, a nested dictionary is a dictionary that contains one or more dictionaries as values. Often, you may need to update the value of a particular key within a nested dictionary. In this tutorial, we will see how to update a value in a nested dictionary using Python.

Let's suppose we have the following nested dictionary:

```python
nested_dict = {
    'person1': {
        'name': 'John',
        'age': 30
    },
    'person2': {
        'name': 'Jane',
        'age': 25
    }
}
```

Now, let's say we want to update the age of 'person1' to 35. Here's how you can do it:

```python
nested_dict['person1']['age'] = 35
```

In the code above, `'person1'` is the key of the outer dictionary, and `'age'` is the key of the inner dictionary. By accessing these keys one after the other, we can update the corresponding value using the assignment operator (`=`).

If the specified key does not exist in the nested dictionary, a `KeyError` will be raised. To handle this, you can either check if the key exists before updating the value using an `if` statement or use the `get()` method to retrieve the value.

Here's an example that demonstrates updating a value in a nested dictionary by verifying the existence of the key:

```python
if 'person1' in nested_dict:
    nested_dict['person1']['age'] = 35
else:
    print("Key 'person1' does not exist.")

```

Alternatively, you can use the `get()` method to update the value:

```python
nested_dict.get('person1', {}).update({'age': 35})
```

In the code above, we are using the `get()` method to retrieve the nested dictionary corresponding to the key `'person1'`. If the key does not exist, `get()` will return an empty dictionary (`{}`). Then, we call the `update()` method on the returned dictionary to update the value.

Updating a value in a nested dictionary in Python is a straightforward process. You need to access each nested level by chaining the keys and then use the assignment operator to update the value.