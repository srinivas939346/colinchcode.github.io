---
layout: post
title: "[python] Using Celery in a Flask application"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to integrate Celery into a Flask application to offload time-consuming tasks and improve the performance of your application.

## Table of Contents
- [What is Celery](#what-is-celery)
- [Setting up Celery](#setting-up-celery)
- [Creating Tasks](#creating-tasks)
- [Running Celery](#running-celery)
- [Conclusion](#conclusion)

## What is Celery
[Celery](https://docs.celeryproject.org/en/stable/) is a distributed task queue system that allows you to run time-consuming tasks in the background asynchronously. It is written in Python and provides great flexibility and scalability.

## Setting up Celery
To use Celery in your Flask application, you need to install it first. You can install Celery using pip:

```console
$ pip install celery
```

Once Celery is installed, you need to configure your Flask application to use it. You can create a Celery instance in your Flask application's factory function or in a separate module. Here's an example of how to create a Celery instance in a separate module:

```python
# celery.py
from celery import Celery
from flask import Flask

def make_celery(app):
    celery = Celery(
        app.import_name,
        broker=app.config['CELERY_BROKER_URL'],
        backend=app.config['CELERY_RESULT_BACKEND']
    )
    celery.conf.update(app.config)

    TaskBase = celery.Task

    class ContextTask(TaskBase):
        abstract = True

        def __call__(self, *args, **kwargs):
            with app.app_context():
                return TaskBase.__call__(self, *args, **kwargs)

    celery.Task = ContextTask
    return celery

app = Flask(__name__)
app.config.update(
    CELERY_BROKER_URL='redis://localhost:6379/0',
    CELERY_RESULT_BACKEND='redis://localhost:6379/0'
)

celery = make_celery(app)
```
In this example, we configure Celery to use Redis as the broker and result backend. You can replace the Redis URLs with the appropriate URLs for your environment.

## Creating Tasks
Now that Celery is set up, you can define tasks that will be executed asynchronously in the background. Tasks are defined as regular Python functions decorated with the `@celery.task` decorator. Here's an example:

```python
# tasks.py
from celery import current_app

@current_app.task
def add_numbers(x, y):
    result = x + y
    return result
```
In this example, we define a task called `add_numbers` that takes two arguments `x` and `y` and returns their sum.

## Running Celery
To run Celery, you need to start a Celery worker process. You can do this by running the following command:

```console
$ celery -A celery worker --loglevel=info
```

This command starts a worker that listens for and executes Celery tasks.

To enqueue tasks from your Flask application, you can use the `delay()` method on the task object. Here's an example:

```python
from your_application import celery
from your_application.tasks import add_numbers

result = add_numbers.delay(5, 10)
```

The `delay()` method enqueues the task for execution and returns a `AsyncResult` object that can be used to check the status and result of the task.

## Conclusion
Integrating Celery into your Flask application can greatly improve its performance by offloading time-consuming tasks to be executed asynchronously in the background. With Celery's flexibility and scalability, you can easily handle large and complex workloads. Happy coding!