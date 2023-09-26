---
layout: post
title: "[python] How to loop through a nested dictionary in Python?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

Looping through a nested dictionary in Python allows you to access and process the data contained within. Here's how you can iterate over a nested dictionary using Python's `for` loop:

```python
data = {
    "key1": {
        "nested_key1": "value1",
        "nested_key2": "value2"
    },
    "key2": {
        "nested_key3": "value3",
        "nested_key4": "value4"
    }
}

# Loop through the outer dictionary
for key, value in data.items():
    print(f"Key: {key}")

    # Loop through the inner dictionary
    for nested_key, nested_value in value.items():
        print(f"Nested Key: {nested_key}")
        print(f"Nested Value: {nested_value}")

        # Access specific values within the inner dictionary
        if nested_key == "nested_key2":
            print(f"Found key 'nested_key2' with value: {nested_value}")
```

In this example, we have a nested dictionary called `data` which contains two outer keys (`"key1"` and `"key2"`) each with their own inner dictionaries. 

Using the first `for` loop, we iterate over the outer dictionary and extract each key-value pair. Then, using the second `for` loop, we iterate over the inner dictionary corresponding to each key and extract the nested key-value pairs.

By accessing the `nested_key` and `nested_value` variables, you can perform various operations or checks within the loop. In the provided example, we check if the `nested_key` is equal to `"nested_key2"` and print its value if it matches.

Feel free to adapt this code to suit your specific use case and perform the necessary actions on the nested dictionary.