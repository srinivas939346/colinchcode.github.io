---
layout: post
title: "[python] Using Apache Kafka as a message broker in Python Celery"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

Apache Kafka is a popular distributed streaming platform that can be used as a message broker in various applications. In this tutorial, we'll explore how to use Apache Kafka as a message broker in a Python Celery application.

## Table of Contents

1. [What is Apache Kafka?](#what-is-apache-kafka)
2. [Installing Apache Kafka](#installing-apache-kafka)
3. [Setting up a Kafka broker](#setting-up-a-kafka-broker)
4. [Setting up Celery](#setting-up-celery)
5. [Using Kafka as Celery's message broker](#using-kafka-as-celerys-message-broker)
6. [Conclusion](#conclusion)

## What is Apache Kafka?

Apache Kafka is a distributed streaming platform that is designed to handle high-throughput, fault-tolerant, and real-time data streams. It provides a pub-sub model where producers publish messages to topics, and consumers subscribe to these topics to receive the messages.

## Installing Apache Kafka

To install Apache Kafka, you can follow the official documentation on the Apache Kafka website. Make sure you have Java installed on your system before proceeding with the installation.

## Setting up a Kafka broker

Once Apache Kafka is installed, you need to set up a Kafka broker that will act as the message broker for your Celery application. Here are the general steps to set up a Kafka broker:

1. Start the ZooKeeper server: Kafka relies on ZooKeeper for maintaining cluster state. Start the ZooKeeper server using the provided script.

2. Start the Kafka server: Start the Kafka server using the provided script. This will start a single-node Kafka cluster.

3. Create a Kafka topic: Use the `kafka-topics.sh` script to create a Kafka topic that will be used to publish and consume messages.

## Setting up Celery

Next, you need to set up Celery in your Python project. Celery is a distributed task queue system that allows you to distribute tasks and process them asynchronously.

To install Celery, you can use pip:

```python
pip install celery
```

## Using Kafka as Celery's message broker

To use Kafka as Celery's message broker, you need to configure Celery to use the Kafka transport. Here's an example configuration using the `kafka` transport:

```python
from celery import Celery

app = Celery('myapp', broker='kafka://localhost:9092')
```

In this example, we configure Celery to use the Kafka broker running on `localhost` with the default Kafka port (`9092`).

Once Celery is configured, you can define tasks and publish them to Kafka topics using Celery's task decorator. Here's an example:

```python
from myapp import app

@app.task
def add(x, y):
    return x + y
```

To publish a task to a Kafka topic, you can use Celery's `delay` method:

```python
add.delay(5, 10)
```

The published tasks will be consumed by Celery workers that are configured to use the same Kafka broker.

## Conclusion

In this tutorial, we explored how to use Apache Kafka as a message broker in a Python Celery application. We covered the steps to install Apache Kafka, set up a Kafka broker, install Celery, and configure Celery to use Kafka as the message broker. Using Kafka with Celery allows you to distribute tasks across multiple workers in a reliable and scalable manner.