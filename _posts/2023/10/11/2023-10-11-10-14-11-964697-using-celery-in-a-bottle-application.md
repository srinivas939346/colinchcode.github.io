---
layout: post
title: "[python] Using Celery in a Bottle application"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

If you are building a web application using the Bottle framework in Python and need to run long-running or asynchronous tasks, Celery is a great choice. Celery is a distributed task queue system that allows you to execute tasks asynchronously in the background.

In this tutorial, we will walk through the process of integrating Celery into a Bottle application.

## Table of Contents
1. [Setting up Celery](#setting-up-celery)
2. [Creating a Celery Task](#creating-a-celery-task)
3. [Running the Celery Worker](#running-the-celery-worker)
4. [Using Celery in Bottle](#using-celery-in-bottle)
5. [Conclusion](#conclusion)

## Setting up Celery
To get started, you will need to install Celery using pip:

```python
pip install celery
```

Next, let's create a `celery.py` file in your project directory to configure Celery:

```python
from celery import Celery

app = Celery('myapp', broker='amqp://guest@localhost//', backend='rpc://')

@app.task
def add(x, y):
    return x + y
```

In the above code, we create a Celery instance with the name 'myapp' and configure the broker and backend. The broker URL specifies the message broker to use for task message passing. Here, we are using the RabbitMQ broker (`amqp://guest@localhost//`). The backend URL specifies the result backend to use. Here, we are using the RPC backend (`rpc://`).

## Creating a Celery Task
Now let's create a task that we can execute asynchronously using Celery. In our `celery.py` file, we define a simple task called `add` that takes two numbers as input and returns their sum.

```python
@app.task
def add(x, y):
    return x + y
```

## Running the Celery Worker
To run the Celery worker, use the following command:

```shell
celery -A celery worker --loglevel=info
```

This command starts the Celery worker that listens for tasks and executes them.

## Using Celery in Bottle
To use Celery in your Bottle application, you will need to import the Celery instance from your `celery.py` file and call the task function.

```python
from bottle import Bottle
from .celery import app, add

app = Bottle()

@app.route('/add/<x:int>/<y:int>')
def add_route(x, y):
    result = add.delay(x, y)
    return f"The result will be available at /result/{result.id}"

@app.route('/result/<task_id>')
def get_result(task_id):
    task = add.AsyncResult(task_id)
    if task.state == 'SUCCESS':
        return f"The result is: {task.result}"
    else:
        return "Task in progress"
```

In our Bottle application, we define two routes. In the `add_route`, we call the `add` task asynchronously using `add.delay(x, y)`. The task is executed in the background, and its result is not immediately available. We return a message with the task ID to the client, indicating that the result will be available at `/result/<task_id>`.

In the `get_result` route, we retrieve the task using `add.AsyncResult(task_id)` and check its state. If the task has completed successfully, we return the result. Otherwise, we return a message indicating that the task is still in progress.

## Conclusion
Using Celery in a Bottle application allows you to easily handle long-running or asynchronous tasks in the background. By following the steps outlined in this tutorial, you can integrate Celery into your Bottle application and execute tasks asynchronously.

To learn more about Celery and Bottle, refer to their official documentation:

- [Celery Documentation](https://docs.celeryproject.org/en/stable/)
- [Bottle Documentation](https://bottlepy.org/docs/dev/)