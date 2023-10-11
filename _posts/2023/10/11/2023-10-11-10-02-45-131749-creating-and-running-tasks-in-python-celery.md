---
layout: post
title: "[python] Creating and running tasks in Python Celery"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

Python Celery is a powerful distributed task queue framework that allows you to asynchronously execute tasks in a distributed and parallel manner. In this blog post, we will explore how to create and run tasks using Celery in Python.

### Table of Contents
1. [Introduction to Celery](#introduction-to-celery)
2. [Installing Celery](#installing-celery)
3. [Creating a Celery project](#creating-a-celery-project)
4. [Creating tasks](#creating-tasks)
5. [Running a Celery worker](#running-a-celery-worker)
6. [Executing tasks](#executing-tasks)
7. [Conclusion](#conclusion)

### Introduction to Celery

Celery is a distributed task queue framework that allows you to handle a large number of tasks asynchronously. It is written in Python and supports multiple message brokers and result backends such as RabbitMQ, Redis, and more.

### Installing Celery

To get started with Celery, you first need to install it. You can use pip to install Celery by running the following command:

```bash
pip install celery
```

### Creating a Celery project

Once Celery is installed, you can create a Celery project by following these steps:

1. Create a new directory for your Celery project.
2. Within the project directory, create a file named `celery.py` which will serve as the Celery configuration file.
3. Open `celery.py` and add the following code:

```python
from celery import Celery

app = Celery('mycelery', broker='pyamqp://guest@localhost//')

```

### Creating tasks

In Celery, tasks are defined as regular Python functions. To create a task, you need to define a function and annotate it with the `@app.task` decorator from Celery.

```python
@app.task
def add(x, y):
    return x + y
```

### Running a Celery worker

To execute tasks in Celery, you need to run a Celery worker which listens to the task queue and executes the tasks as they arrive. To start a Celery worker, use the following command:

```bash
celery -A celery_project worker --loglevel=info
```

### Executing tasks

To execute a task in Celery, you need to import the task and call it as you would call a regular function.

```python
from celery_project import add

result = add.delay(4, 5)
print(result.get())
```

The `delay()` method kicks off the execution of the task and returns an AsyncResult object. Use the `get()` method to retrieve the result of the task. You can also use the `get()` method with a timeout value to wait for the task to complete.

### Conclusion

Celery is a powerful distributed task queue framework that allows you to handle a large number of tasks asynchronously. In this blog post, we have learned how to create and run tasks in Python Celery. We covered the process of installing Celery, creating a Celery project, defining tasks, running a Celery worker, and executing tasks. With Celery, you can easily scale your application and improve its performance by offloading time-consuming tasks to background workers.