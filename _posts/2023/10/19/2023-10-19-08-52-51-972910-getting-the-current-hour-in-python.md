---
layout: post
title: "[python] Getting the current hour in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

```python
import datetime

# Get the current datetime
now = datetime.datetime.now()

# Extract the hour from the datetime
current_hour = now.hour

# Print the current hour
print("Current hour:", current_hour)
```

In this code, we import the `datetime` module and use the `now()` function to get the current date and time. Then, we use the `hour` attribute of the `datetime` object to extract the current hour. Finally, we print the current hour.

This code will output something like:

```
Current hour: 15
```

Remember to format your code according to the conventions of the programming language you are using.