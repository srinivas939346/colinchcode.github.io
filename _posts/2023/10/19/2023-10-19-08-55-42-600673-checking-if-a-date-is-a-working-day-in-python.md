---
layout: post
title: "[python] Checking if a date is a working day in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

When working with dates in Python, you may come across the need to check if a given date is a working day or not. This can be useful when calculating business days or determining if a certain operation should be performed on a specific date.

In Python, you can achieve this by utilizing the `datetime` module along with the `pytz` library to handle time zones. Here's an example code snippet that demonstrates how to check if a date is a working day in Python:

```python
import datetime
import pytz

def is_working_day(date):
    # Get the current time in UTC
    now = datetime.datetime.now(pytz.UTC)
  
    # Check if the given date is a weekend day
    if date.weekday() >= 5:
        return False

    # Check if the given date is a holiday
    # Replace `holidays` with your own list of holidays
    holidays = [
        datetime.date(date.year, 1, 1),   # New Year's Day
        datetime.date(date.year, 12, 25),  # Christmas Day
    ]
    if date in holidays:
        return False

    # Check if the given date is in the future
    if date > now.date():
        return False

    # If none of the conditions above are met, the date is a working day
    return True

# Usage example
date_to_check = datetime.datetime(2022, 5, 16).date()
if is_working_day(date_to_check):
    print(f"{date_to_check} is a working day.")
else:
    print(f"{date_to_check} is not a working day.")
```

In this example, the `is_working_day` function takes a `date` as input and checks various conditions to determine if it is a working day or not. 

It first checks if the date falls on a weekend (Saturday or Sunday) by using the `weekday()` method, which returns an integer representing the day of the week. If the weekday is 5 (Saturday) or 6 (Sunday), it immediately returns `False`.

Next, it checks if the date is a holiday by comparing it with a list of predefined holidays. You can modify this list to include your own holidays or use a library like `holidays` for a more comprehensive list of holidays for different countries.

After that, it checks if the date is in the future by comparing it with the current date using the `now()` method from `datetime.datetime` with UTC as the time zone.

If none of the conditions above are met, the date is considered a working day and the function returns `True`.

To test the function, you can create a `datetime` object representing the date you want to check and pass it to the `is_working_day` function. The function will return `True` if it is a working day, and `False` otherwise.

Remember to replace `holidays` with your own list of holidays or use a suitable holiday library for your region.

By using this code snippet, you can easily check if a given date is a working day in Python.