---
layout: post
title: "[python] Getting the current day in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

In this blog post, we will discuss how to get the current day in Python. 

To get the current day, we can make use of the `datetime` module in Python. The `datetime` module provides various classes and methods to work with dates and times.

Here is an example code snippet that demonstrates how to get the current day:

```python
from datetime import datetime

# Get the current date and time
current_date = datetime.now()

# Extract the day from the current date
current_day = current_date.day

# Print the current day
print("Current day:", current_day)
```

In the above code, we first import the `datetime` module. Then, we use the `now()` method to get the current date and time. We can then extract the day from the current date using the `day` attribute. Finally, we print the current day using the `print()` function.

When you run the code, it will output the current day like this:

```
Current day: 15
```

You can customize the output format by using the `strftime()` method of the `datetime` object. This method allows you to specify a format string to represent the date and time in a specific format.

For example, if you want to display the current day in a different format like "Tuesday", you can modify the code as follows:

```python
from datetime import datetime

# Get the current date and time
current_date = datetime.now()

# Extract the day name from the current date
current_day = current_date.strftime("%A")

# Print the current day
print("Current day:", current_day)
```

By using the `%A` format code, the `strftime()` method will return the full name of the day.

Make sure to check the [Python datetime documentation](https://docs.python.org/3/library/datetime.html) for more information on working with dates and times in Python.

That's it! You now know how to get the current day in Python using the `datetime` module. We hope you found this blog post helpful.