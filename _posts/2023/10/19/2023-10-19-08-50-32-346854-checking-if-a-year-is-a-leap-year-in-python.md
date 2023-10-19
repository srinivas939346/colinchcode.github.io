---
layout: post
title: "[python] Checking if a year is a leap year in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

In this blog post, we will discuss how to check if a given year is a leap year using Python. A leap year is a year that is evenly divisible by 4, except for years that are evenly divisible by 100. However, years that are evenly divisible by 400 are leap years.

## Table of Contents
- [Leap Year](#leap-year)
- [Checking Leap Year in Python](#checking-leap-year-in-python)
- [Example Code](#example-code)
- [Conclusion](#conclusion)

## Leap Year

A leap year is a year that has an extra day, 29th February. The purpose of the leap year is to keep our calendar in alignment with the Earth's revolutions around the Sun. Without the extra day every four years, our calendar would gradually shift out of sync with the solar year.

## Checking Leap Year in Python

To check if a year is a leap year in Python, we can use the following conditions:

1. If a year is evenly divisible by 4, it is a leap year.
2. If a year is evenly divisible by 100, it is not a leap year, unless it is also divisible by 400.

By following these conditions, we can accurately determine if a given year is a leap year or not.

## Example Code

```python
def is_leap_year(year):
    if year % 4 == 0:
        if year % 100 == 0:
            if year % 400 == 0:
                return True
            else:
                return False
        else:
            return True
    else:
        return False

# Testing the function
year = 2020
if is_leap_year(year):
    print(f"{year} is a leap year!")
else:
    print(f"{year} is not a leap year!")
```

In the above code, we have defined a function `is_leap_year` that takes a `year` as an argument and returns `True` if it is a leap year, otherwise `False`. We then test the function by passing a year (`2020`) to it and printing the respective output.

## Conclusion

In this blog post, we have discussed how to check if a given year is a leap year in Python. We have defined the conditions for a year to be considered a leap year and provided an example code snippet to demonstrate the implementation. By using this code, you can easily determine whether a given year is a leap year or not in Python.