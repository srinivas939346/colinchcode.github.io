---
layout: post
title: "[python] Calculating the number of days between two dates in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

When working with dates in Python, there might be a need to calculate the number of days between two dates. Luckily, Python provides built-in functions to make this task easy. In this article, you will learn different approaches to calculate the number of days between two dates in Python.

## Using the `datetime` module

The `datetime` module in Python provides the `date` class, which can be used to represent dates. To calculate the number of days between two dates, follow these steps:

1. Import the `datetime` module.
2. Create two instances of the `date` class representing the desired dates.
3. Subtract the first date from the second date to get a `timedelta` object.
4. Access the `days` attribute of the `timedelta` object to get the number of days between the two dates.

Here's an example code snippet that demonstrates this approach:

```python
from datetime import date

# Create date instances
date1 = date(2021, 1, 1)
date2 = date(2021, 12, 31)

# Calculate the difference
delta = date2 - date1

# Get the number of days
num_of_days = delta.days

print(num_of_days)  # Output: 364
```

In this example, we create two `date` instances representing January 1, 2021, and December 31, 2021. We then calculate the difference between the two dates and access the `days` attribute of the `timedelta` object to get the number of days.

## Using the `dateutil` module

Another approach to calculate the number of days between two dates is by using the `dateutil` module. The `dateutil` module provides a powerful function called `relativedelta`, which can handle more complex date calculations.

To use this approach, follow these steps:

1. Install the `python-dateutil` package, if not already installed, using pip: `pip install python-dateutil`.
2. Import the `date` and `relativedelta` classes from the `dateutil` module.
3. Create two instances of the `date` class.
4. Use the `relativedelta` function to calculate the difference between the two dates.
5. Access the `days` attribute of the `relativedelta` object to get the number of days.

Here's an example code snippet that demonstrates this approach:

```python
from datetime import date
from dateutil.relativedelta import relativedelta

# Create date instances
date1 = date(2021, 1, 1)
date2 = date(2021, 12, 31)

# Calculate the difference
delta = relativedelta(date2, date1)

# Get the number of days
num_of_days = delta.days

print(num_of_days)  # Output: 364
```

In this example, we create two `date` instances representing the same dates as before. We then use the `relativedelta` function to calculate the difference between the two dates and access the `days` attribute to get the number of days.

## Conclusion

Calculating the number of days between two dates in Python is made easy with the help of the `datetime` and `dateutil` modules. Whether you choose to use the `datetime` module or the `dateutil` module, both methods provide a straightforward way to perform this task. Feel free to use the one that suits your needs the best!

## References

- [Python `datetime` module documentation](https://docs.python.org/3/library/datetime.html)
- [Python `dateutil` module documentation](https://dateutil.readthedocs.io/en/stable/)