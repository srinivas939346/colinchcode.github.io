---
layout: post
title: "[python] Getting the weekday name for a specific date in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

```python
import datetime

# Define the date you want to get the weekday name for
date = datetime.date(2022, 1, 1)

# Get the weekday number (0 - Monday, 6 - Sunday)
weekday_num = date.weekday()

# Get the weekday name
weekday_name = date.strftime('%A')

# Print the weekday name
print(f"The weekday name for {date} is {weekday_name}")
```

In the above code, we first import the `datetime` module. Then, we define the date we want to get the weekday name for using the `datetime.date` class. In this example, we set the date to January 1, 2022.

Next, we use the `weekday()` method of the `date` object to get the weekday number. The weekday number is an integer ranging from 0 to 6, where 0 represents Monday and 6 represents Sunday.

Finally, we use the `strftime()` method of the `date` object to format the date into the weekday name string using the `%A` directive. The `%A` directive represents the full weekday name.

We then print the weekday name using f-string formatting.

When you run the above code, it will output:

```
The weekday name for 2022-01-01 is Saturday
```

You can change the date in the code to get the weekday name for different dates.

I hope this helps! Let me know if you have any further questions.

**References:**
- [Python datetime module documentation](https://docs.python.org/3/library/datetime.html)