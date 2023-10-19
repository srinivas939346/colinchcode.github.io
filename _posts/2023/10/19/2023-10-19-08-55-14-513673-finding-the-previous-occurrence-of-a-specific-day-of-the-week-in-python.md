---
layout: post
title: "[python] Finding the previous occurrence of a specific day of the week in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

When working with date and time in Python, it is often necessary to find the previous occurrence of a specific day of the week. For example, you might need to determine the date of the last Monday or the previous Friday.

In this article, we will explore a couple of ways to achieve this using Python's built-in `datetime` module. 

## Method 1: Using datetime and timedelta

The `datetime` module provides a convenient way to manipulate dates and times. We can use the `datetime` class along with the `timedelta` class to find the previous occurrence of a specific day of the week.

Here's an example that demonstrates how to find the previous occurrence of a specific day of the week:

```python
import datetime

# Specify the desired day of the week
target_day = datetime.datetime.strptime('Monday', '%A').date().weekday()

# Get the current date
current_date = datetime.date.today()

# Calculate the difference between the current day and the target day
days_to_subtract = (current_date.weekday() - target_day) % 7

# Calculate the previous occurrence of the target day
previous_occurrence = current_date - datetime.timedelta(days=days_to_subtract)

# Print the previous occurrence
print(previous_occurrence)
```

In this example, we first specify the desired day of the week (`Monday` in this case) using `strptime` and the `%A` format code. We then get the current date using `date.today()`.

Next, we calculate the difference between the current day of the week and the target day using modulo 7 to handle wrapping around the days of the week. This gives us the number of days to subtract from the current date.

Finally, we subtract the number of days from the current date using `timedelta` and print the previous occurrence.

## Method 2: Using dateutil library

Alternatively, we can use the `dateutil` library, which provides some additional functionality for working with dates and times.

To use `dateutil`, you'll need to install it first. You can do this by running `pip install python-dateutil`.

Here's how you can find the previous occurrence of a specific day of the week using `dateutil`:

```python
from datetime import datetime
from dateutil.relativedelta import relativedelta, MO

# Specify the desired day of the week
target_day = MO(-1)

# Get the current date
current_date = datetime.now().date()

# Calculate the previous occurrence of the target day
previous_occurrence = current_date + relativedelta(weekday=target_day)

# Print the previous occurrence
print(previous_occurrence)
```

In this example, we use `relativedelta` from `dateutil.relativedelta` to calculate the previous occurrence of a specific day of the week. We specify the desired day of the week as `MO(-1)`, which represents the last Monday.

We then use `datetime.now().date()` to get the current date, and add `relativedelta(weekday=target_day)` to get the previous occurrence of the target day.

## Conclusion

Finding the previous occurrence of a specific day of the week is a common task when working with date and time in Python. In this article, we explored two methods using Python's `datetime` module and the `dateutil` library.

Whether you choose to use the `datetime` module or the `dateutil` library, both methods provide convenient ways to calculate the previous occurrence of a specific day of the week based on the current date.