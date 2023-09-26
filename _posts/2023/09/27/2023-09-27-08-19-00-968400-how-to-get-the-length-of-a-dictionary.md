---
layout: post
title: "[python] How to get the length of a dictionary?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

In Python, you can use the built-in function `len()` to get the length or size of a dictionary. 

Here's an example:

```python
# Define a dictionary
my_dict = {'apple': 3, 'banana': 5, 'orange': 2}

# Get the length of the dictionary
dict_length = len(my_dict)

# Print the length
print("The length of the dictionary is:", dict_length)
```

Output:
```
The length of the dictionary is: 3
```

In the above code, the `len()` function is used to find the number of key-value pairs in the dictionary. It returns an integer representing the length.

Remember, the length of a dictionary is determined by the number of key-value pairs it contains, not the total number of elements within the values.