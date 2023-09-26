---
layout: post
title: "[python] How to access values in a nested dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

In Python, dictionaries are a powerful data structure that allow you to store key-value pairs. Sometimes, you may encounter nested dictionaries, where a dictionary contains another dictionary as a value. Accessing values in such nested dictionaries might seem a bit tricky at first, but it's actually quite straightforward.

Let's say we have the following nested dictionary:

```python
data = {
    'person1': {
        'name': 'John',
        'age': 30,
        'city': 'New York'
    },
    'person2': {
        'name': 'Jane',
        'age': 25,
        'city': 'London'
    }
}
```

To access the value of a specific key inside a nested dictionary, you can simply chain the key access operators (`[]`) together.

For example, to access the `name` value of `person1`, you can use the following code:

```python
name = data['person1']['name']
print(name)
```

This will output:

```
John
```

Similarly, you can access other values in the nested dictionary in a similar manner. For instance, to access the `city` value of `person2`:

```python
city = data['person2']['city']
print(city)
```

This will output:

```
London
```

By chaining the key access operators, you can access values in nested dictionaries to any level of depth. Just make sure to provide the correct keys in the correct order.

In case a key does not exist, accessing it directly will throw a `KeyError`. To handle such situations, you can utilize the `get()` method, which allows you to specify a default value to return if the key does not exist.

Here's an example using `get()`:

```python
city = data.get('person3', {}).get('city', 'Unknown')
print(city)
```

This will output:

```
Unknown
```

In the above code, `data.get('person3', {})` returns an empty dictionary because `'person3'` does not exist in the `data` dictionary. Then, `{}.get('city', 'Unknown')` returns the default value `'Unknown'` because `'city'` does not exist in the empty dictionary.

So, by using the `get()` method, you can handle cases where a key may not exist in a nested dictionary.

That's it! You now know how to access values in a nested dictionary in Python.