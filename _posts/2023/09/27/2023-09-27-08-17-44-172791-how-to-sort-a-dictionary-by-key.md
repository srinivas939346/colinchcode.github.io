---
layout: post
title: "[python] How to sort a dictionary by key?"
description: " "
date: 2023-09-27
tags: [python]
comments: true
share: true
---

```
# Create a dictionary
fruits = {'apple': 3, 'banana': 2, 'cherry': 5, 'date': 1}

# Sort the dictionary by keys
sorted_fruits = dict(sorted(fruits.items()))

# Print sorted dictionary
print(sorted_fruits)
```

Output:
```
{'apple': 3, 'banana': 2, 'cherry': 5, 'date': 1}
```

In the example above, we have a dictionary called `fruits` containing four key-value pairs. By using the `items()` method, we can get a list of key-value tuples representing the dictionary. We then pass this list to the `sorted()` function, which sorts it based on the keys. Finally, we convert the sorted list of tuples back into a dictionary using the `dict()` function.

After executing the code snippet, you will see that the `sorted_fruits` dictionary is sorted alphabetically by key.

Sorting a dictionary by key can be useful in scenarios where you need to iterate through the dictionary in a specific order or perform other operations that require sorted keys.