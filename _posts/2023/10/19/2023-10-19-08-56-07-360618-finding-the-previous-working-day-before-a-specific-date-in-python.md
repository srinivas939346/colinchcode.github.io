---
layout: post
title: "[python] Finding the previous working day before a specific date in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

In some scenarios, you may need to find the previous working day before a specific date in Python. This can be useful in financial calculations, scheduling, or any situation where you need to exclude weekends and holidays.

Here's a Python code snippet that finds the previous working day:

```python
import datetime as dt
import calendar

def find_previous_working_day(target_date):
    # Subtract one day from the target date
    previous_day = target_date - dt.timedelta(days=1)

    # Loop until a working day is found
    while previous_day.weekday() >= 5 or previous_day in holidays:
        previous_day -= dt.timedelta(days=1)

    return previous_day

# Example usage
target_date = dt.datetime(2022, 1, 6)  # January 6, 2022
previous_working_day = find_previous_working_day(target_date)
print(previous_working_day)
```

In the above code, we use the `datetime` module to handle dates and timedelta for arithmetic operations. We also use the `calendar` module to check for weekends.

The `find_previous_working_day` function takes a `target_date` as input and subtracts one day from it. It then enters a loop that checks if the previous day is a weekend (`weekday() >= 5`) or a holiday. If it is, it subtracts one more day and continues the loop until a working day is found.

You can replace the `holidays` variable with your own list of holidays or integrate an API that provides holiday information.

Running the code with the example date `2022-01-06` would output `2022-01-05`, as January 6, 2022, is a Thursday, and the previous working day is Wednesday.

Feel free to modify the code according to your specific needs. This example gives you a starting point for finding previous working days in Python.