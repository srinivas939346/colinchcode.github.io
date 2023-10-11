---
layout: post
title: "[python] Using Celery in a Django application"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to use Celery, an asynchronous task queue library, in a Django application. Celery is commonly used to offload time-consuming tasks to improve the performance and scalability of web applications.

By utilizing Celery, we can delegate long-running or computationally expensive tasks to worker processes, while our Django application remains responsive to user requests. Let's jump right in!

## Table of Contents
1. [What is Celery?](#what-is-celery)
2. [Setting up Celery in Django](#setting-up-celery)
3. [Defining and Running Tasks](#defining-and-running-tasks)
4. [Monitoring Celery](#monitoring-celery)
5. [Conclusion](#conclusion)

## What is Celery? 

Celery is an open-source distributed task queue framework implemented in Python. It allows the execution of tasks asynchronously across multiple workers or machines. With Celery, you can perform tasks in the background, such as sending emails, generating reports, or performing complex calculations, without blocking the main application.

## Setting up Celery in Django

To get started with Celery in Django, we need to perform a few steps to integrate it into our project:

1. Install Celery: You can install Celery using pip:
   ```shell
   pip install celery
   ```

2. Configure Celery in `settings.py`: Add the following configuration settings to your Django application's settings:
   ```python
   CELERY_BROKER_URL = 'redis://localhost:6379/0'
   CELERY_RESULT_BACKEND = 'redis://localhost:6379/0'
   ```

3. Create a `celery.py` file: Create a new file named `celery.py` in your Django project directory alongside `settings.py` with the following content:
   ```python
   from __future__ import absolute_import, unicode_literals
   import os
   from celery import Celery

   os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'your_project.settings')

   app = Celery('your_project')
   app.config_from_object('django.conf:settings', namespace='CELERY')
   app.autodiscover_tasks()
   ```

4. Initialize Celery in `__init__.py`: Open the `__init__.py` file inside your Django project directory and add the following code:
   ```python
   from .celery import app as celery_app

   __all__ = ('celery_app',)
   ```

5. Start Celery worker: Open a terminal, navigate to your Django project directory, and run the following command to start the Celery worker:
   ```shell
   celery -A your_project worker --loglevel=info
   ```

## Defining and Running Tasks

Once Celery is set up, you can define and run tasks in your Django application. A task is a Python function that performs a specific job. Let's define a sample task to send an email asynchronously:

```python
from django.core.mail import send_mail
from celery import shared_task

@shared_task
def send_async_email(subject, message, recipient_list):
    send_mail(subject, message, 'noreply@example.com', recipient_list)
```

To run this task, import it wherever you want to use it and call it like this:

```python
from your_app.tasks import send_async_email

send_async_email.delay('Subject', 'Message', ['user@example.com'])
```

## Monitoring Celery

Celery provides a monitoring feature through its Flower package. Flower is a web-based monitoring tool that allows us to view the status and statistics of Celery workers and tasks. To install Flower, run the following command:

```shell
pip install flower
```

To start the Flower server, navigate to your project directory and run the following:

```shell
celery -A your_project flower
```

You can now access the Flower monitoring dashboard by visiting `http://localhost:5555` in your browser.

## Conclusion

With Celery, you can easily perform time-consuming tasks asynchronously in your Django application, helping improve performance and user experience. By following the steps outlined in this blog post, you can integrate Celery into your Django project and leverage its powerful features.

Remember to configure Celery properly, define and run your tasks, and monitor their execution using Flower. Stay scalable and responsive with Celery in your Django application!

Happy coding!