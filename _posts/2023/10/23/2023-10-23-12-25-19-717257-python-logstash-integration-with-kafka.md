---
layout: post
title: "[python] Python Logstash integration with Kafka"
description: " "
date: 2023-10-23
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to integrate Python with Logstash and Kafka to build a powerful and scalable logging system. Logstash is a popular open-source data processing tool, while Kafka is a distributed streaming platform.

## Table of Contents
- [Introduction](#introduction)
- [Setting up Logstash](#setting-up-logstash)
- [Configuring Kafka](#configuring-kafka)
- [Python Integration](#python-integration)
- [Sending Logs to Kafka](#sending-logs-to-kafka)

## Introduction

Logstash acts as a central pipeline for ingesting, processing, and forwarding logs. Kafka provides a reliable and fault-tolerant messaging system that helps to handle high data throughput. By combining these two technologies, we can create a robust logging infrastructure.

## Setting up Logstash

First, let's set up Logstash. Install Logstash by following the official documentation for your operating system. Once installed, create a configuration file `logstash.conf` with the following content:

```
input {
  kafka {
    bootstrap_servers => "localhost:9092"
    topics => ["logs"]
    group_id => "logstash"
    consumer_threads => 3
    codec => json
  }
}

output {
  stdout {
    codec => rubydebug
  }
}
```

This configuration specifies that Logstash should consume messages from the Kafka `logs` topic, using the `json` codec, and print the processed logs to the console.

## Configuring Kafka

Next, we need to set up Kafka. Install Kafka by following the official documentation for your operating system. Start Kafka and create a topic named `logs` using the following command:

```
bin/kafka-topics.sh --create --topic logs --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
```

## Python Integration

To integrate Python with Logstash and Kafka, we will use the `python-logstash` library. Install it using `pip`:

```bash
pip install python-logstash
```

## Sending Logs to Kafka

Now, let's write a Python script to send logs to Kafka. Create a file named `kafka_logger.py` with the following code:

``` python
import logging
import logstash

logger = logging.getLogger()
logger.setLevel(logging.INFO)
logger.addHandler(logstash.TCPLogstashHandler('localhost', 5959))

logger.info("Hello, Logstash and Kafka!")
```

In this code, we configure a logger with the Logstash host and port. We then send a log message using the `logger.info()` method.

To run this script, ensure that both Logstash and Kafka are running. Execute the Python script using the command:

```bash
python kafka_logger.py
```

The log message will be sent to the Kafka topic `logs` and consumed by Logstash. You will see the processed log output on the console.

## Conclusion

We have successfully integrated Python with Logstash and Kafka to build a powerful logging system. This combination provides a flexible and scalable solution for processing and analyzing logs. Feel free to explore more advanced features and customization options offered by Logstash and Kafka to enhance your logging infrastructure.

## References
- [Logstash Documentation](https://www.elastic.co/logstash)
- [Kafka Documentation](https://kafka.apache.org/documentation/)
- [python-logstash Library](https://github.com/vklochan/python-logstash)