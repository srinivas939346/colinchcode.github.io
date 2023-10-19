---
layout: post
title: "[python] Finding the next working day after a specific date in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

In this blog post, we will discuss how to find the next working day after a specific date in Python. Sometimes, it is important to skip weekends or holidays when calculating dates, especially in applications like scheduling or booking systems. We will demonstrate a simple and efficient way to achieve this.

## Table of Contents
1. [Using datetime and timedelta](#using-datetime-and-timedelta)
2. [Considering weekends](#considering-weekends)
3. [Skipping holidays](#skipping-holidays)
4. [Complete code example](#complete-code-example)
5. [Conclusion](#conclusion)

## Using datetime and timedelta <a name="using-datetime-and-timedelta"></a>

Python provides the `datetime` module that makes working with dates and times straightforward. To find the next working day, we can use the `timedelta` class from this module. The `timedelta` object represents a duration or difference between two dates or times.

Let's start by importing the necessary modules:

```python
import datetime
from datetime import timedelta
```

Next, let's define a function that takes a specific date as input and returns the next working day:

```python
def find_next_working_day(date):
    next_day = date + timedelta(days=1)
    return next_day
```

In the above code, we add one day to the input date using the `timedelta` class. This gives us the next day. Now, let's move on to considering weekends.

## Considering weekends <a name="considering-weekends"></a>

If we want to skip weekends and find the next working day, we need to check if the next day falls on a Saturday or Sunday. If it does, we should continue to the next day until we find a working day.

Let's modify our function to skip weekends:

```python
def find_next_working_day(date):
    next_day = date + timedelta(days=1)
    
    while next_day.weekday() >= 5:  # Saturday is 5th day, Sunday is 6th day
        next_day += timedelta(days=1)
    
    return next_day
```

In this updated code, we use a `while` loop to keep adding one day until we reach a non-weekend day (i.e., weekday less than 5).

## Skipping holidays <a name="skipping-holidays"></a>

To skip holidays, we need a list of holiday dates. We can create a simple list of holiday dates or use a more sophisticated approach like fetching the holiday data from an API or a database.

Let's assume we have a `holidays` list containing holiday dates. We can update the function to skip holidays as follows:

```python
def find_next_working_day(date):
    next_day = date + timedelta(days=1)
    
    while next_day.weekday() >= 5 or next_day in holidays:
        next_day += timedelta(days=1)
    
    return next_day
```

In the above code, we add an additional condition in the `while` loop to check if the `next_day` is in the `holidays` list.

## Complete code example <a name="complete-code-example"></a>

Here is the complete code example:

```python
import datetime
from datetime import timedelta

holidays = [datetime.datetime(2022, 1, 1), datetime.datetime(2022, 12, 25)]  # Example list of holiday dates

def find_next_working_day(date):
    next_day = date + timedelta(days=1)
    
    while next_day.weekday() >= 5 or next_day in holidays:
        next_day += timedelta(days=1)
    
    return next_day

# Example usage
start_date = datetime.datetime(2022, 1, 1)
next_working_day = find_next_working_day(start_date)
print(next_working_day)
```

## Conclusion <a name="conclusion"></a>

In this blog post, we have learned how to find the next working day after a specific date in Python. We used the `datetime` module and the `timedelta` class to achieve this. By considering weekends and holidays, we can ensure accurate calculations of working dates in various applications. Feel free to customize the code according to your specific requirements.