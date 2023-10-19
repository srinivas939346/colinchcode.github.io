---
layout: post
title: "[python] Checking if two dates are equal in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

```python
from datetime import date

# Creating two date objects
date1 = date(2021, 5, 15)
date2 = date(2021, 5, 15)

# Checking if the dates are equal
if date1 == date2:
    print('The dates are equal')
else:
    print('The dates are not equal')
```

In the above example, we import the `date` class from the `datetime` module. We then create two `date` objects, `date1` and `date2`, representing two different dates. We use the `==` operator to compare the two dates, and if they are equal, we print a message stating that the dates are equal. Otherwise, we print a message stating that the dates are not equal.

Keep in mind that when comparing dates, they need to be of the same type (in this case, both `date` objects).