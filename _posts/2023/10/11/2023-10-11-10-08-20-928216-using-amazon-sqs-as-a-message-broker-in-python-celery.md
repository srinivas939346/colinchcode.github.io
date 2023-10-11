---
layout: post
title: "[python] Using Amazon SQS as a message broker in Python Celery"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to use Amazon Simple Queue Service (SQS) as a message broker in Python Celery. Celery is a distributed task queue system that allows you to perform asynchronous tasks in your Python applications. Amazon SQS is a fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications.

## Table of Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Setting up Amazon SQS](#setting-up-amazon-sqs)
- [Configuring Celery to Use SQS](#configuring-celery-to-use-sqs)
- [Creating and Running Celery Tasks](#creating-and-running-celery-tasks)
- [Conclusion](#conclusion)

## Introduction
Celery provides support for various message brokers, including RabbitMQ, Redis, and SQS. By using SQS as the message broker in Celery, you can leverage the scalability and reliability of SQS for asynchronous task processing in your Python applications.

## Prerequisites
Before getting started, make sure you have the following prerequisites:
- An Amazon Web Services (AWS) account
- Python installed on your local machine
- The `boto3` library installed (`pip install boto3`)
- Celery installed (`pip install celery`)

## Setting up Amazon SQS
To use SQS as the message broker for Celery, you need to create an SQS queue in your AWS account. Here are the steps to set up SQS:

1. Log in to the AWS Management Console and open the SQS service.
2. Click "Create Queue" to create a new queue.
3. Provide a name for your queue and specify any required settings.
4. Once the queue is created, note down the queue URL. You will need it later to configure Celery.

## Configuring Celery to Use SQS
After setting up Amazon SQS, you need to configure Celery to use SQS as the message broker. 

In your Python code, create a Celery configuration file (e.g., `celeryconfig.py`) with the following content:

```python
# celeryconfig.py
broker_url = 'sqs://<your-queue-url>'
result_backend = 'rpc'
```

Replace `<your-queue-url>` with the actual URL of your SQS queue.

## Creating and Running Celery Tasks
Now that you have configured Celery to use SQS, you can create and run Celery tasks as usual. Here's an example:

```python
from celery import Celery

app = Celery('tasks')
app.config_from_object('celeryconfig')

@app.task
def add_numbers(x, y):
    return x + y
```

To run the Celery worker, use the following command in your terminal:

```bash
celery -A tasks worker --loglevel=info
```

To enqueue the task for execution, you can call it using `apply_async()`, as shown below:

```python
from tasks import add_numbers

result = add_numbers.apply_async(args=(4, 5))
```

The task will be sent to the SQS queue and processed by the Celery worker.

## Conclusion
In this blog post, we have seen how to use Amazon SQS as a message broker in Python Celery. By leveraging SQS's scalability and reliability, you can enhance the asynchronous task processing capabilities of your Python applications.