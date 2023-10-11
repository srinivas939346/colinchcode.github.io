---
layout: post
title: "[python] Using Django ORM as a result backend in Python Celery"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

Celery is a popular distributed task queue system for Python. It allows you to perform time-consuming tasks asynchronously in the background. One of the key features of Celery is the ability to use different result backends to store the task results.

In this blog post, we will discuss how to use the Django ORM as a result backend in Python Celery.

## Table of Contents
- [Introduction](#introduction)
- [Configuring Celery](#configuring-celery)
- [Setting up Django ORM as a Result Backend](#setting-up-django-orm-as-a-result-backend)
- [Using the Django ORM Result Backend](#using-the-django-orm-result-backend)
- [Conclusion](#conclusion)

## Introduction
Celery provides various result backends like Redis, RabbitMQ, and SQLAlchemy. However, if you are already using Django in your project, it is convenient to use the Django ORM as the result backend since you don't need to configure an additional system for storing task results.

## Configuring Celery
To use Celery in your Django project, you need to install the `celery` package and configure it. Here's a basic configuration example:

```python
# settings.py

CELERY_BROKER_URL = 'amqp://localhost'  # URL for the message broker
CELERY_RESULT_BACKEND = 'django-db'  # Result backend using Django ORM
```

## Setting up Django ORM as a Result Backend
To use the Django ORM as a result backend, you need to create a Django model to store the task results. For example, let's create a `TaskResult` model in your Django app's models file:

```python
# models.py

from django.db import models

class TaskResult(models.Model):
    task_id = models.CharField(max_length=255, primary_key=True)
    result = models.TextField()
    status = models.CharField(max_length=50)
```

Run migrations to create the necessary table in your database:

```shell
$ python manage.py makemigrations
$ python manage.py migrate
```

## Using the Django ORM Result Backend
Once you have set up the Django ORM as a result backend, you can use it in your Celery tasks by importing and using the `task` decorator provided by Celery:

```python
# tasks.py

from celery import task
from myapp.models import TaskResult

@task
def my_long_task():
    # Perform some long-running task
    result = 42

    # Save the task result using Django ORM
    task_result = TaskResult(task_id=my_long_task.request.id, result=result, status="completed")
    task_result.save()

    return result
```

Now you can call the `my_long_task` task and retrieve the result later:

```python
# some_module.py

from myapp.models import TaskResult
from tasks import my_long_task

# Call the task
result = my_long_task.delay()

# Retrieve the result later
task_result = TaskResult.objects.get(task_id=result.task_id)
print(task_result.result)  # 42
```

## Conclusion
In this blog post, we discussed how to use the Django ORM as a result backend in Python Celery. By leveraging the power of the Django ORM, you can easily store and retrieve task results without any additional setup. This integration makes it convenient for Django projects to use Celery for handling asynchronous tasks efficiently.