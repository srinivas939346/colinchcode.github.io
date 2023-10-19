---
layout: post
title: "[python] Finding the number of weekends in a specific month in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---
Are you looking for a way to calculate the number of weekends in a specific month using Python? In this blog post, we will explore a simple solution to this problem.

## Table of Contents
- [Approach](#approach)
- [Example](#example)

## Approach
To find the number of weekends in a specific month, we can utilize the `calendar` module in Python. The `calendar.monthrange(year, month)` function returns a tuple containing the first weekday of the month (0 for Monday, 6 for Sunday) and the number of days in the month.

We can iterate through all the days in the month and check if a given day is a weekend by checking if its weekday is either 5 or 6 (Saturday or Sunday). By counting the number of weekend days, we will obtain the desired result.

## Example
Let's say we want to find the number of weekends in January 2022. Here's how we can do it in Python:

```python
import calendar

def count_weekends(year, month):
    _, num_days = calendar.monthrange(year, month)
    count = 0
    
    for day in range(1, num_days+1):
        weekday = calendar.weekday(year, month, day)
        
        if weekday == 5 or weekday == 6:
            count += 1
    
    return count

# Usage example
num_weekends = count_weekends(2022, 1)
print(f"The number of weekends in January 2022 is: {num_weekends}")
```

In this example, we define a function `count_weekends` that takes the `year` and `month` as parameters. We use `calendar.monthrange` to get the number of days in the month. Then, we iterate through each day, obtain its weekday using `calendar.weekday`, and increment the count if it is a weekend. Finally, we return the count.

Running the code will output the number of weekends in the specified month, which in this case is January 2022.

## Conclusion
Calculating the number of weekends in a specific month in Python is straightforward using the `calendar` module. By using the provided code, you can easily find the number of weekends in any desired month.

I hope you found this blog post helpful! If you have any questions or suggestions, feel free to leave a comment below.

## References
- [Python calendar module documentation](https://docs.python.org/3/library/calendar.html)