---
layout: post
title: "[python] Scheduling tasks in Python Celery"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

Celery is a powerful and widely used task queue library for Python. One of its key features is the ability to schedule tasks to run at specified times or intervals. In this blog post, we will explore how to schedule tasks in Python Celery.

## Table of Contents

1. [Installing Celery](#installing-celery)
2. [Configuring Celery](#configuring-celery)
3. [Scheduling Tasks](#scheduling-tasks)
4. [Periodic Scheduling](#periodic-scheduling)
5. [Conclusion](#conclusion)

## Installing Celery

To get started, we need to install Celery. You can install it via pip:

```python
pip install celery
```

## Configuring Celery

Once Celery is installed, we need to configure it to work with our application. Create a `celery.py` file in your project directory and add the following code:

```python
from celery import Celery

app = Celery('myapp', broker='pyamqp://guest@localhost//')
```

This code creates a Celery instance named `app` and configures it to use the RabbitMQ message broker.

## Scheduling Tasks

To schedule a task in Celery, we need to define the task and annotate it with the `@app.task` decorator.

```python
@app.task
def send_email(to, subject, body):
    # Code to send email
    pass
```

Now, we can schedule the task to run at a specific time using the `apply_async` method of the task.

```python
from datetime import datetime, timedelta

scheduled_time = datetime.now() + timedelta(minutes=10)
send_email.apply_async(args=['example@example.com', 'Test Email', 'Hello, World!'], eta=scheduled_time)
```

In the example above, we schedule the `send_email` task to run after 10 minutes from the current time.

## Periodic Scheduling

Celery also provides support for scheduling tasks to run periodically. To schedule a task to run at fixed intervals, we can use Celery's `beat` scheduler.

Create a `celeryconfig.py` file in your project directory and add the following code:

```python
from celery.schedules import crontab

CELERYBEAT_SCHEDULE = {
    'every-minute': {
        'task': 'tasks.send_email',
        'schedule': crontab(minute='*')
    },
}
```

This code configures a periodic task that will run the `send_email` task every minute.

To start the Celery scheduler, run the following command:

```bash
celery -A myapp beat
```

The scheduler will now execute the scheduled tasks as per the defined schedule.

## Conclusion

In this blog post, we learned how to schedule tasks in Python Celery. We explored scheduling tasks at specific times using `apply_async` and periodic scheduling using Celery's `beat` scheduler. Celery provides a flexible and robust framework for managing task schedules in Python applications.