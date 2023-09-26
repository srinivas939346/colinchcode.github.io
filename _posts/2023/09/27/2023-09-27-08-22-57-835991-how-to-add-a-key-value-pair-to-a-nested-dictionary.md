---
layout: post
title: "[python] How to add a key-value pair to a nested dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

Meta Description: Learn how to add a key-value pair to a nested dictionary in Python using simple and efficient code.

Keywords: Python, dictionary, nested dictionary, key-value pair, add, update, nested data structure, code example

---

In Python, dictionaries are a powerful data structure for storing and organizing key-value pairs. With nested dictionaries, you can create more complex data structures to represent hierarchical data. In this tutorial, we will explore how to add a key-value pair to a nested dictionary in Python.

Let's say we have the following nested dictionary:

```python
my_dict = {
    'person1': {
        'name': 'John',
        'age': 25
    },
    'person2': {
        'name': 'Jane',
        'age': 30
    }
}
```

To add a new key-value pair, let's say 'gender': 'male', to the nested dictionary `my_dict['person1']`, we can use the following code:

```python
my_dict['person1']['gender'] = 'male'
```

This line of code accesses the inner dictionary `my_dict['person1']` and adds a new key `'gender'` with the value `'male'`.

Now, the updated `my_dict` will look as follows:

```python
{
    'person1': {
        'name': 'John',
        'age': 25,
        'gender': 'male'
    },
    'person2': {
        'name': 'Jane',
        'age': 30
    }
}
```

To make the code more robust, you can use the `dict.setdefault()` method. This method first checks if the specified key exists in the dictionary. If the key is present, it returns the corresponding value. Otherwise, it adds the key with the provided default value.

Here's an example using the `setdefault()` method to add the key `'gender'` with the value `'male'`:

```python
my_dict['person1'].setdefault('gender', 'male')
```

The `setdefault()` method retains the existing value if the key is already present. So, it is useful when you want to add a key only if it does not already exist.

Adding key-value pairs to nested dictionaries in Python is straightforward, thanks to the flexibility and simplicity of the language.

In summary, to add a key-value pair to a nested dictionary in Python, you can directly access the inner dictionary using indexing and assign the key-value pair. Alternatively, you can use the `setdefault()` method to add the key-value pair with a default value if the key does not already exist.

Happy coding!