---
layout: post
title: "[python] Python Logstash integration with RabbitMQ"
description: " "
date: 2023-10-23
tags: [python]
comments: true
share: true
---

In this post, we will discuss how to integrate Logstash with RabbitMQ using Python. Logstash is a popular open-source tool used for collecting, parsing, and storing logs for analysis. RabbitMQ is a widely used message broker that allows different applications to communicate with each other.

## Prerequisites

Before we proceed, make sure you have the following prerequisites:

- Python installed on your system
- RabbitMQ server up and running
- Logstash installed

## Setting Up RabbitMQ

To begin, let's first set up RabbitMQ. Follow these steps:

1. Install RabbitMQ by downloading it from the official website and following the installation instructions for your operating system.

2. Start the RabbitMQ server.

## Setting Up Logstash

Next, we need to set up Logstash. Follow these steps:

1. Install Logstash by downloading it from the official website and following the installation instructions for your operating system.

2. Create a Logstash configuration file (e.g., `logstash.conf`) with the following content:
```conf
input {
  rabbitmq {
    hosts => ["localhost"]
    queue => "logs"
    durable => true
    codec => "json"
  }
}

output {
  stdout {
    codec => "json"
  }
}
```
This configuration tells Logstash to consume messages from the "logs" queue in RabbitMQ and print them to the console.

3. Start Logstash using the configuration file:
```bash
$ logstash -f logstash.conf
```

## Python Integration

Now that RabbitMQ and Logstash are set up, let's integrate them using Python. We will use the `pika` library, which is a Python client for RabbitMQ.

1. Install the `pika` library:
```bash
$ pip install pika
```

2. Create a Python script (e.g., `log_publisher.py`) with the following code:

```python
import pika
import logging

logging.basicConfig(level=logging.INFO)

def publish_logs():
    connection = pika.BlockingConnection(pika.ConnectionParameters('localhost'))
    channel = connection.channel()

    channel.queue_declare(queue='logs', durable=True)

    logs = [
        {"message": "Log message 1"},
        {"message": "Log message 2"},
        {"message": "Log message 3"}
    ]

    for log in logs:
        channel.basic_publish(
            exchange='',
            routing_key='logs',
            body=log,
            properties=pika.BasicProperties(
                delivery_mode=2  # Make messages persistent
            )
        )
        logging.info(f"Published log: {log['message']}")

    connection.close()

if __name__ == '__main__':
    publish_logs()
```

In this script, we establish a connection with RabbitMQ, declare the "logs" queue, and publish some log messages to the queue.

3. Run the Python script:
```bash
$ python log_publisher.py
```

You should see the log messages being published in the console.

## Conclusion

In this post, we learned how to integrate Logstash with RabbitMQ using Python. We set up RabbitMQ and Logstash, and then used the `pika` library to publish log messages to RabbitMQ. This integration allows you to feed logs into Logstash for further processing and analysis.

By following these steps, you can effectively integrate Logstash and RabbitMQ in your Python-based logging infrastructure.

References:
- [Logstash documentation](https://www.elastic.co/guide/en/logstash/current/index.html)
- [RabbitMQ documentation](https://www.rabbitmq.com/documentation.html)
- [pika library documentation](https://pika.readthedocs.io/en/stable/)