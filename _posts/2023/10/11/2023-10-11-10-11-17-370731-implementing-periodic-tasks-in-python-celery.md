---
layout: post
title: "[python] Implementing periodic tasks in Python Celery"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

Celery is a popular distributed task queue framework in Python that allows you to distribute tasks across multiple workers. In addition to distributing tasks, Celery also provides support for scheduling and running periodic tasks. This can be useful for automating repetitive tasks or running scheduled jobs.

In this blog post, we will explore how to implement periodic tasks using Celery in Python.

## Table of Contents
- [Introduction to Celery](#introduction-to-celery)
- [Installing Celery](#installing-celery)
- [Creating a Celery Task](#creating-a-celery-task)
- [Scheduling Periodic Tasks](#scheduling-periodic-tasks)
- [Running the Celery Worker](#running-the-celery-worker)
- [Conclusion](#conclusion)

## Introduction to Celery

Celery is a distributed task queue framework for Python that can be used to handle and distribute tasks asynchronously. It supports various message brokers like RabbitMQ, Redis, and more, allowing you to scale and distribute tasks across multiple workers.

## Installing Celery

To get started, we need to install Celery. You can install Celery using pip by running the following command:

```bash
pip install celery
```

## Creating a Celery Task

Before we can schedule a periodic task, we need to create a Celery task. A Celery task is a Python function that performs a specific job. It can be any normal Python function, decorated with the `@task` decorator from the Celery library.

Here's an example of a Celery task that prints "Hello, World!" when executed:

```python
from celery import Celery

app = Celery('tasks', broker='redis://localhost:6379/0')

@app.task
def hello_world():
    print("Hello, World!")
```

## Scheduling Periodic Tasks

Now that we have created a Celery task, we can schedule it to run periodically. Celery uses a separate scheduler called `beat` for scheduling periodic tasks. To configure the scheduler, we need to create a file called `celerybeat.py` and define the scheduling settings.

Here's an example of a `celerybeat.py` file that schedules the `hello_world` task to run every 5 seconds:

```python
from celery import Celery
from celery.schedules import crontab

app = Celery('tasks', broker='redis://localhost:6379/0')

app.conf.beat_schedule = {
    'hello-world-every-5-seconds': {
        'task': 'tasks.hello_world',
        'schedule': 5.0,
    },
}

if __name__ == '__main__':
    app.start()
```

In the above example, we define a single schedule entry named `hello-world-every-5-seconds`. The `task` property specifies the task to be executed (in this case, `tasks.hello_world`), and the `schedule` property defines the frequency at which the task should run (5.0 seconds in this case).

## Running the Celery Worker

To start the Celery worker and scheduler, we need to run the following command:

```bash
celery -A tasks worker --beat --loglevel=info
```

This command starts the Celery worker and the scheduler (`beat`). The `--loglevel` option sets the logging level to `info`, displaying detailed information about task execution.

## Conclusion

In this blog post, we learned how to implement periodic tasks using Celery in Python. We saw how to create a Celery task, schedule it to run periodically, and run the Celery worker and scheduler. Celery provides a powerful and flexible way to automate repetitive tasks and schedule jobs in Python applications.

For more information on Celery, you can refer to the official [Celery documentation](http://docs.celeryproject.org). Happy task scheduling!