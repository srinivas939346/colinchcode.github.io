---
layout: post
title: "[python] Using Redis as a message broker in Python Celery"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

![Redis Logo](https://redis.io/images/redis-logo.png)

Message brokers play a crucial role in distributed systems by facilitating communication between different components. One popular message broker is Redis, which offers high performance and low latency. In this blog post, we will explore how to use Redis as a message broker in Python Celery, a distributed task queue framework.

## Table of Contents

1. [Introduction](#introduction)
2. [Setting up Redis](#setting-up-redis)
3. [Installing Celery](#installing-celery)
4. [Configuring Celery with Redis](#configuring-celery-with-redis)
5. [Publishing and Consuming Messages](#publishing-and-consuming-messages)
6. [Conclusion](#conclusion)

## Introduction

Celery allows you to distribute the execution of tasks across multiple workers, making it a powerful tool for building scalable and efficient systems. By using Redis as the message broker, Celery can distribute tasks to multiple workers and ensure that each task is executed exactly once.

## Setting up Redis

Before we begin, make sure you have Redis installed and running on your system. You can visit the Redis website and follow the installation instructions for your operating system.

## Installing Celery

To use Celery in your Python project, you need to install it using pip, the package installer for Python. Open your terminal or command prompt and run the following command:

```shell
pip install celery
```

## Configuring Celery with Redis

To configure Celery to use Redis as the message broker, you need to update your Celery configuration file. Create a new file called `celery.py` in your project directory and add the following code:

```python
from celery import Celery

app = Celery('myapp', broker='redis://localhost:6379/0')
```

In the above code, we create a new Celery instance with the name `myapp` and specify the Redis URL as the broker. You can replace `localhost` and `6379` with the appropriate Redis hostname and port if necessary.

## Publishing and Consuming Messages

Once you have configured Celery with Redis, you can start publishing and consuming messages using Celery's task decorators. Here's an example using a simple task:

```python
from celery import Celery

app = Celery('myapp', broker='redis://localhost:6379/0')

@app.task
def add(x, y):
    return x + y
```

In the code above, we define a task named `add` that takes two arguments `x` and `y`. When this task is called, it will calculate the sum of `x` and `y`.

To publish a message, you can use the `delay` method provided by the task decorator. For example:

```python
add.delay(2, 3)
```

This will send the message to the Redis broker and Celery will route it to an available worker for execution.

To consume messages, you need to start a Celery worker. Open a new terminal or command prompt window and run the following command:

```shell
celery -A myapp worker --loglevel=info
```

The worker will connect to the Redis broker and start consuming messages. You will see the output in the terminal window whenever a task is executed.

## Conclusion

Using Redis as a message broker in Python Celery allows you to build scalable and efficient distributed systems. In this blog post, we covered the basics of setting up Redis, installing Celery, configuring Celery to use Redis as the message broker, and publishing and consuming messages. Now you have a solid foundation to start building your own distributed tasks using Celery and Redis.

Happy coding!