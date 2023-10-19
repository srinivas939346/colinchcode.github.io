---
layout: post
title: "[python] Sorting a list of dates in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

Let's assume you have a list of dates represented as strings in the format "YYYY-MM-DD". Here's an example:

```python
dates = ["2022-01-15", "2021-12-25", "2022-03-10", "2022-02-05"]

sorted_dates = sorted(dates)
print(sorted_dates)
```

Output:
```
['2021-12-25', '2022-01-15', '2022-02-05', '2022-03-10']
```

In the code above, we used the `sorted()` function to create a new list `sorted_dates` which contains the sorted version of the `dates` list. The resulting output is a list of dates sorted in ascending order.

If you want to sort the dates in descending order, you can use the `reverse` parameter of the `sort()` function or pass `reverse=True` to the `sorted()` function:

```python
dates.sort(reverse=True)
print(dates)
```

Output:
```
['2022-03-10', '2022-02-05', '2022-01-15', '2021-12-25']
```

In this case, the original `dates` list is sorted in descending order.

If you want to sort the dates based on a specific criterion such as the day or month, you can use a lambda function as the `key` parameter. For example, to sort the dates based on the day:

```python
dates = ["2022-01-15", "2021-12-25", "2022-03-10", "2022-02-05"]

sorted_dates = sorted(dates, key=lambda x: x.split('-')[2])
print(sorted_dates)
```

Output:
```
['2021-12-25', '2022-02-05', '2022-01-15', '2022-03-10']
```

In this example, the lambda function `lambda x: x.split('-')[2]` extracts the day component of each date string and uses it for sorting.

Sorting a list of dates in Python is straightforward using the `sort()` or `sorted()` functions combined with the `key` parameter. Experiment with different sorting criteria to meet your specific requirements.