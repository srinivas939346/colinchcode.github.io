---
layout: post
title: "[python] Getting the current second in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

```python
import datetime

current_time = datetime.datetime.now()
current_second = current_time.second

print("Current second:", current_second)
```

In the code above, we import the `datetime` module and then use the `now()` method to get the current date and time. We store this in the `current_time` variable. To extract the second from the current time, we access the `second` attribute of the `current_time` object and store it in the `current_second` variable.

Finally, we print the value of `current_second`, which represents the current second.

You can run this code and see the output that displays the current second.

References:
- Python `datetime` module documentation: [https://docs.python.org/3/library/datetime.html](https://docs.python.org/3/library/datetime.html)