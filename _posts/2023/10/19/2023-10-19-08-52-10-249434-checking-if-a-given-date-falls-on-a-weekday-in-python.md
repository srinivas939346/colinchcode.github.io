---
layout: post
title: "[python] Checking if a given date falls on a weekday in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

Sometimes, we need to check if a given date falls on a weekday or a weekend. In Python, we can use the `datetime` module to accomplish this task very easily. 

Here's an example of how to check if a given date falls on a weekday in Python:

```python
import datetime

def is_weekday(date):
    """
    Check if a given date falls on a weekday.
    
    Args:
        date (str): The date to check in 'YYYY-MM-DD' format.
    
    Returns:
        bool: True if the date falls on a weekday, False otherwise.
    """
    
    year, month, day = map(int, date.split('-'))
    given_date = datetime.date(year, month, day)
    
    return given_date.weekday() < 5
```

In this example, we define a function called `is_weekday` that takes a date as input in the format 'YYYY-MM-DD'. We split the date into year, month, and day components and then create a `datetime.date` object from these components.

We then use the `weekday()` method of the `datetime.date` object, which returns an integer representing the day of the week, where Monday is 0 and Sunday is 6. We compare this value to 4 (since 5 and 6 represent the weekend) and return `True` if the value is less than 5, indicating that the date falls on a weekday.

Here's an example of how to use this function:

```python
date = '2021-10-15'
if is_weekday(date):
    print(f"{date} falls on a weekday.")
else:
    print(f"{date} falls on a weekend.")
```

In this example, the given date is '2021-10-15', which is a Friday. The function `is_weekday` returns `True`, indicating that the date falls on a weekday, and the program outputs "2021-10-15 falls on a weekday."

References:
- [Python datetime module](https://docs.python.org/3/library/datetime.html)