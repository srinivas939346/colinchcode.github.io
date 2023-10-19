---
layout: post
title: "[python] Displaying the current date and time in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

In this tutorial, we will look at how to display the current date and time in Python using the `datetime` module.

## Table of Contents
- [Introduction](#introduction)
- [Displaying the Current Date](#displaying-the-current-date)
- [Displaying the Current Time](#displaying-the-current-time)
- [Displaying the Current Date and Time](#displaying-the-current-date-and-time)
- [Conclusion](#conclusion)

## Introduction
Python provides the `datetime` module to work with dates and times. It allows us to easily retrieve the current date and time and display them as per our requirements.

## Displaying the Current Date
To display the current date, we can use the `date` class from the `datetime` module. Here is an example:

```python
import datetime

current_date = datetime.date.today()
print("Current date:", current_date)
```

The output will be in the format `YYYY-MM-DD`, representing the current date.

## Displaying the Current Time
To display the current time, we can use the `datetime` class from the `datetime` module. Here is an example:

```python
import datetime

current_time = datetime.datetime.now().time()
print("Current time:", current_time)
```

The output will be in the format `HH:MM:SS.MMMMMM`, representing the current time.

## Displaying the Current Date and Time
To display both the current date and time together, we can use the `datetime` class from the `datetime` module. Here is an example:

```python
import datetime

current_datetime = datetime.datetime.now()
print("Current date and time:", current_datetime)
```

The output will be in the format `YYYY-MM-DD HH:MM:SS.MMMMMM`, representing the current date and time.

## Conclusion
In this tutorial, we learned how to display the current date and time in Python using the `datetime` module. You can now use this knowledge to incorporate date and time functionality into your Python programs.