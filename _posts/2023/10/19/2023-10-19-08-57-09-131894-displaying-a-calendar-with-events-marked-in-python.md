---
layout: post
title: "[python] Displaying a calendar with events marked in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

Managing events and calendars is a common requirement in many applications. In this tutorial, we will explore how to display a calendar with marked events using Python.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installing Required Packages](#installing-required-packages)
- [Creating the Calendar](#creating-the-calendar)
- [Adding Events](#adding-events)
- [Displaying the Calendar](#displaying-the-calendar)
- [Conclusion](#conclusion)
- [References](#references)

## Prerequisites

Before we begin, make sure you have Python installed on your system. You can download and install Python from the official website (https://www.python.org/downloads/).

## Installing Required Packages

To create a calendar with marked events, we will be using the `calendar` and `datetime` modules in Python, which are part of the standard library. There is no need to install any additional packages.

## Creating the Calendar

We can start by creating a basic calendar using the `calendar` module. We will also define a function to get the month and year from the user.

```python
import calendar

def get_month_year():
    month = int(input("Enter the month (1-12): "))
    year = int(input("Enter the year: "))
    
    return month, year

def create_calendar(month, year):
    cal = calendar.monthcalendar(year, month)

    # Customize calendar layout here

    return cal

month, year = get_month_year()
cal = create_calendar(month, year)
```

In the above code, `get_month_year()` function prompts the user to enter a month and year. The `calendar.monthcalendar()` function returns a list of lists representing the calendar for the specified month and year.

## Adding Events

Next, we'll add the functionality to mark events on the calendar. We can create a dictionary to store the events and update the calendar accordingly. Let's define a function to add events.

```python
def add_event(cal):
    day = int(input("Enter the day: "))
    event = input("Enter the event: ")

    cal[0][day-1] = f"({day}) {event}"
    return cal

cal = add_event(cal)
```

In the `add_event()` function, we prompt the user to enter the day and event. We update the calendar by replacing the day's number with the formatted event string.

## Displaying the Calendar

To display the calendar with marked events, we can iterate over the calendar list and print each row.

```python
def display_calendar(cal):
    for week in cal:
        formatted_week = [str(day) if day != 0 else " " for day in week]
        print(" | ".join(formatted_week))

display_calendar(cal)
```

The `display_calendar()` function iterates over each week in the calendar. If the day is not 0, it prints the day's number; otherwise, it prints an empty space. The `join()` function is used to combine the formatted days with a separator.

## Conclusion

In this tutorial, we learned how to create a calendar with marked events in Python. We explored how to create the calendar, add events, and display the final calendar.

Feel free to customize the calendar layout, add more features, or integrate it into your own applications.

## References

- Python documentation: [calendar](https://docs.python.org/3/library/calendar.html)
- Python documentation: [datetime](https://docs.python.org/3/library/datetime.html)