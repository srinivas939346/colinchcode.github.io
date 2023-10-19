---
layout: post
title: "[python] Checking if a date is a holiday in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

## Table of Contents
- [Install the `holidays` Library](#install-the-holidays-library)
- [Check if a Date is a Holiday](#check-if-a-date-is-a-holiday)

### Install the `holidays` Library

To start, we need to install the `holidays` library. Open your terminal or command prompt and run the following command:

```bash
pip install holidays
```

### Check if a Date is a Holiday

Once the library is installed, we can use it to check if a given date is a holiday. Let's see an example:

```python
import holidays
from datetime import date

# Create a list of countries for which we want to check holidays
countries = ['US', 'Germany', 'Italy']

# Create a date object for the date we want to check
check_date = date(2022, 1, 1)

# Loop through each country and check if the date is a holiday
for country in countries:
    if check_date in holidays.CountryHoliday(country, prov=None, state=None):
        print(f"{check_date} is a holiday in {country}")
    else:
        print(f"{check_date} is not a holiday in {country}")
```

In this example, we first import the necessary modules. We then create a list of countries for which we want to check holidays. Next, we create a `date` object for the date we want to check, in this case, January 1, 2022. 

We then loop through each country in the list and use the `in` keyword to check if the `check_date` is present in the list of holidays for that country. If it is, we print a message stating that the date is a holiday. Otherwise, we print a message stating that it is not a holiday.

By running this code, you will get the result indicating whether the given date is a holiday in each country.

### Conclusion

In this blog post, we learned how to check if a date is a holiday in Python using the `holidays` library. This can be useful in various applications where you need to handle holidays differently or need to determine whether a business will be closed on a specific date. The `holidays` library provides a convenient way to handle this task for different countries.