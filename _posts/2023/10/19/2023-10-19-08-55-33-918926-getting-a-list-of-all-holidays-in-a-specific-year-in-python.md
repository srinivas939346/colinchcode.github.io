---
layout: post
title: "[python] Getting a list of all holidays in a specific year in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

In this tutorial, we will learn how to use the `holidays` library in Python to get a list of all holidays in a specific year.

## Table of Contents
- [Installations](#installations)
- [Getting Started](#getting-started)
- [Getting Holidays for a Specific Year](#getting-holidays-for-a-specific-year)
- [Customizing Holiday Parameters](#customizing-holiday-parameters)
- [Conclusion](#conclusion)
- [References](#references)

## Installations

To get started, we need to install the `holidays` library. Open your terminal and run the following command:

```shell
pip install holidays
```

## Getting Started

First, let's import the necessary libraries:

```python
import holidays
```

## Getting Holidays for a Specific Year

To get a list of all holidays for a specific year, we can create an instance of the `CountryHoliday` class and pass the country code as an argument. 

Let's get all holidays in the United States for the year 2022:

```python
us_holidays = holidays.UnitedStates(years=2022)
```

Next, we can iterate over the `us_holidays` object to print all the holidays:

```python
for date, name in sorted(us_holidays.items()):
    print(f"{date}: {name}")
```

This will display output like:

```
2022-01-01: New Year's Day
2022-01-17: Martin Luther King Jr. Day
2022-02-21: Washington's Birthday
...
```

## Customizing Holiday Parameters

The `holidays` library allows customizing the holiday parameters by passing them as arguments. For example, to exclude a specific holiday, we can use the `exclude` parameter.

Let's get all holidays in Germany for the year 2022, excluding New Year's Day:

```python
de_holidays = holidays.Germany(years=2022, exclude=["New Year's Day"])
```

We can further customize the parameters based on the `holidays` library documentation.

## Conclusion

In this tutorial, we learned how to use the `holidays` library in Python to get a list of all holidays in a specific year. We also explored how to customize the holiday parameters. This can be useful for various applications, such as generating a holiday calendar or calculating business days.

## References

- `holidays` library: [https://pypi.org/project/holidays/](https://pypi.org/project/holidays/)
- `holidays` library documentation: [https://pypi.org/project/holidays/#documentation](https://pypi.org/project/holidays/#documentation)