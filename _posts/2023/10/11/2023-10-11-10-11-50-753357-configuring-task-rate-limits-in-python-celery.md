---
layout: post
title: "[python] Configuring task rate limits in Python Celery"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

Task rate limits are useful when working with the Celery distributed task queue framework in Python. They allow you to control the maximum number of tasks that can be executed per second, minute, hour, or day. Configuring task rate limits is particularly helpful in scenarios where you need to enforce certain constraints on task execution rates to prevent overload or improve system responsiveness.

In this blog post, we will explain how to configure task rate limits in Celery using Python. We will cover both global rate limiting and per-task rate limiting.

### Table of Contents
1. [Global Task Rate Limits](#global-task-rate-limits)
2. [Per-Task Rate Limits](#per-task-rate-limits)

### Global Task Rate Limits<a name="global-task-rate-limits"></a>

To set global rate limits for all tasks in Celery, you need to modify the Celery configuration file (`celery.py` or `celery_app.py`) by adding the `CELERY_DEFAULT_RATE_LIMIT` setting.

1. Open your Celery configuration file.
2. Add the following line:

```python
CELERY_DEFAULT_RATE_LIMIT = '<limit>'
```

Replace `<limit>` with your desired rate limit value. For example, if you want to limit the rate to 10 tasks per second, set it as:

```python
CELERY_DEFAULT_RATE_LIMIT = '10/s'
```

3. Save the configuration file.

After restarting your Celery worker, the global rate limit will be applied to all tasks.

### Per-Task Rate Limits<a name="per-task-rate-limits"></a>

In addition to setting a global rate limit for all tasks, you can also specify individual rate limits for specific tasks. This can be useful when certain tasks require a different rate limit than others.

To set per-task rate limits, you can use the `rate_limit` decorator provided by Celery. Here's how you can do it:

```python
from celery import Celery

app = Celery('myapp')

@app.task(bind=True)
@app.rate_limit('5/m')  # Set the rate limit for this task
def my_task(self):
    # Task logic goes here
```

In the example above, the `rate_limit` decorator is used to set a rate limit of 5 tasks per minute for the `my_task` function. You can adjust the rate limit value according to your requirements and use different units such as per second (`/s`), per minute (`/m`), per hour (`/h`), or per day (`/d`).

Restart your Celery worker after adding or modifying the per-task rate limit decorators for the changes to take effect.

### Conclusion

Configuring task rate limits in Python Celery is a straightforward process that allows you to control the rate of task execution in your application. By setting global rate limits or per-task rate limits, you can prevent overload and ensure better system responsiveness. Consider applying appropriate rate limits to your tasks to optimize the performance of your Celery-based application.