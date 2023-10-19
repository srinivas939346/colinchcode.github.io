---
layout: post
title: "[python] Calculating the age in years based on a birth date in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

In this tutorial, we will learn how to calculate the age in years based on a given birth date using Python.

## Table of Contents
- [Using the `datetime` module](#using-the-datetime-module)
- [Using the `dateutil` module](#using-the-dateutil-module)

## Using the `datetime` module
The `datetime` module in Python provides classes for working with dates and times. We can use the `datetime` module to calculate the age based on the current date and the birth date.

Here's an example using the `datetime` module:

```python
from datetime import datetime

def calculate_age(birth_date):
    current_date = datetime.now()
    age = current_date.year - birth_date.year

    if (current_date.month, current_date.day) < (birth_date.month, birth_date.day):
        age -= 1

    return age

# Example usage
birth_date = datetime(1990, 5, 15)
age = calculate_age(birth_date)
print(f"The age is {age} years")
```

In this example, we define a `calculate_age` function that takes a `birth_date` parameter. We obtain the current date using `datetime.now()`. We subtract the year of the birth date from the current year to get the initial age. Then, we compare the current month and day with the birth month and day. If the current month and day are less than the birth month and day, we subtract 1 from the age. Finally, we return the calculated age.

## Using the `dateutil` module
The `dateutil` module is a flexible date and time library that provides various functions to parse, calculate, and manipulate dates and times. We can use the `dateutil` module to calculate the age based on the current date and the birth date.

To install the `dateutil` module, you can use the following command:

```bash
pip install python-dateutil
```

Here's an example using the `dateutil` module:

```python
from datetime import datetime
from dateutil.relativedelta import relativedelta

def calculate_age(birth_date):
    current_date = datetime.now()
    age = relativedelta(current_date, birth_date).years

    return age

# Example usage
birth_date = datetime(1990, 5, 15)
age = calculate_age(birth_date)
print(f"The age is {age} years")
```

In this example, we import the `relativedelta` class from the `dateutil.relativedelta` module. We define a `calculate_age` function that takes a `birth_date` parameter. We obtain the current date using `datetime.now()` and calculate the age using the `relativedelta` function by passing the current date and the birth date. Finally, we return the calculated age.

## Conclusion
In this tutorial, we have learned how to calculate the age in years based on a given birth date in Python. We explored two different approaches using the `datetime` and `dateutil` modules. You can choose either approach based on your specific requirements. Happy coding!