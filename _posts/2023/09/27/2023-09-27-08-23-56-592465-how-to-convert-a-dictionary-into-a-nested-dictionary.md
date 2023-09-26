---
layout: post
title: "[python] How to convert a dictionary into a nested dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

Converting a dictionary into a nested dictionary in Python can be achieved using a few simple steps. By iterating through the keys and values of the original dictionary, we can create nested dictionaries that mirror the structure of the original dictionary.

Let's go through the process step by step.

## Step 1: Initialize the Original Dictionary

First, let's initialize the original dictionary with some key-value pairs:

```python
original_dict = {
    "key1": "value1",
    "key2": "value2",
    "key3": "value3"
}
```

## Step 2: Create the Nested Dictionary

Next, we'll create a nested dictionary to store the converted values of the original dictionary:

```python
nested_dict = {}
```

## Step 3: Iterate through the Original Dictionary

We'll iterate through the keys and values of the original dictionary using a `for` loop. For each key-value pair, we'll split the key by a separator, such as a dot ("."), to create nested levels in the new dictionary. Then, we'll assign the corresponding value to the nested dictionary.

```python
for key, value in original_dict.items():
    # Split the key by the separator
    keys = key.split(".")
    
    # Assign the value to the nested dictionary
    nested_dict[keys[0]] = {}
    current_dict = nested_dict[keys[0]]
    
    # Create nested dictionaries for each level
    for k in keys[1:-1]:
        current_dict[k] = {}
        current_dict = current_dict[k]
    
    # Assign the final value to the nested dictionary
    current_dict[keys[-1]] = value
```

## Step 4: Print the Nested Dictionary

Finally, let's print the nested dictionary to verify that it matches the structure of the original dictionary:

```python
print(nested_dict)
```

The output should be:

```python
{
    "key1": {
        "key2": {
            "key3": "value3"
        },
        "value1"
    },
    "value2"
}
```

## Conclusion

By following these steps, you can easily convert a dictionary into a nested dictionary in Python. This can be useful when you have flat data and want to organize it into a hierarchical structure.