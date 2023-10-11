---
layout: post
title: "[python] Setting up Python Celery"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

Celery is a powerful distributed task queue system written in Python. It allows you to distribute tasks across multiple worker nodes, making it ideal for running asynchronous tasks and background processing in your Python applications.

In this blog post, we will walk through the steps to set up Celery in Python and get started with running background tasks.

## Table of Contents
- [Installation](#installation)
- [Basic Setup](#basic-setup)
- [Defining Tasks](#defining-tasks)
- [Running the Worker](#running-the-worker)
- [Scheduling Tasks](#scheduling-tasks)
- [Conclusion](#conclusion)

## Installation

Start by installing Celery using pip:

```python
pip install celery
```

You will also need a message broker such as RabbitMQ or Redis to handle task queues. Install RabbitMQ by following the official documentation or use Redis if you prefer. Also, make sure to install the respective Celery broker library:

```python
pip install celery[redis]  # for Redis
pip install celery[rabbitmq]  # for RabbitMQ
```

## Basic Setup

To use Celery in your Python application, you need to create a Celery instance and configure it properly. Here's a basic setup:

```python
from celery import Celery

app = Celery('myapp')
app.config_from_object('celeryconfig')
```

In the code snippet above, we create an instance of Celery called `app`. The `'myapp'` argument is the name of your application. You can replace it with a more appropriate name for your project.

The `config_from_object()` method allows you to load configuration from a module or object. You can define various Celery settings in a separate `celeryconfig.py` file:

```python
broker_url = 'redis://localhost:6379/0'
result_backend = 'redis://localhost:6379/0'
```

Make sure to update the `broker_url` and `result_backend` with the appropriate connection details for your message broker.

## Defining Tasks

Celery allows you to define tasks as Python functions. These tasks can be executed asynchronously by the Celery worker nodes. Here's an example of a simple task:

```python
@app.task
def add(x, y):
    return x + y
```

In the code snippet above, we define a task called `add` that takes two arguments `x` and `y` and returns their sum. The `@app.task` decorator is used to register the function as a Celery task.

## Running the Worker

To run Celery worker nodes, use the `celery` command-line tool. Here's an example command to start a worker:

```shell
celery -A myapp worker --loglevel=info
```

In the command above, replace `myapp` with the name of your application. The `--loglevel` option specifies the logging level of the worker.

## Scheduling Tasks

Celery also provides a convenient way to schedule tasks to run at specified times. You can use the `apply_async()` method to schedule a task. Here's an example:

```python
from datetime import timedelta
from myapp.tasks import add

add.apply_async(args=(4, 6), eta=datetime.now() + timedelta(seconds=10))
```

In the code snippet above, we import the `add` task and use the `apply_async()` method to schedule it to run 10 seconds from now.

## Conclusion

Setting up Python Celery is relatively straightforward and provides a robust solution for running background tasks in your Python applications. By following the steps outlined in this blog post, you can now harness the power of distributed task queues and improve the performance and scalability of your applications.