---
layout: post
title: "[python] Python Logstash integration with Docker"
description: " "
date: 2023-10-23
tags: [python]
comments: true
share: true
---

![Docker logo](https://www.docker.com/sites/default/files/d8/styles/role_icon/public/2019-07/horizontal-logo-monochromatic-white.png)

## Table of Contents

- [Introduction](#introduction)
- [Setting Up Logstash](#setting-up-logstash)
- [Python Logstash Integration](#python-logstash-integration)
- [Conclusion](#conclusion)
- [References](#references)

## Introduction

In modern software development, logging is an essential part of monitoring and debugging applications. Docker, a popular containerization platform, provides a convenient way to package and deploy applications. Combining Docker with a powerful logging tool like Logstash can greatly enhance the logging capabilities of your applications. In this blog post, we will explore how to integrate Logstash with Docker using Python.

## Setting Up Logstash

Before we can integrate Logstash with our Python application running in Docker, we need to set up Logstash as a separate service. Follow these steps to set up Logstash:

1. Install Logstash on your machine or a server. You can download Logstash from the official website: [https://www.elastic.co/logstash](https://www.elastic.co/logstash).

2. Configure Logstash by creating a `logstash.conf` file. This configuration file defines the input, filters, and output for Logstash. You will need to specify the input source (e.g., a log file or a network socket), any filters you want to apply, and the output destination (e.g., Elasticsearch or a database). Refer to the Logstash documentation for more configuration options: [https://www.elastic.co/guide/en/logstash/current/configuration.html](https://www.elastic.co/guide/en/logstash/current/configuration.html).

3. Start Logstash with your configuration file. Use the following command to start Logstash: `logstash -f path/to/logstash.conf`.

Once Logstash is up and running, it will listen for incoming logs based on the specified configuration.

## Python Logstash Integration

To integrate Logstash with our Python application running in Docker, we will use the `python-logstash` library. This library provides a Python logging handler that sends log records to Logstash over a network socket.

Follow these steps to integrate Logstash into your Python application:

1. Install the `python-logstash` library using `pip`:

```shell
$ pip install python-logstash
```

2. Import the `logstash` module in your Python code:

```python
import logging
import logstash
```

3. Configure the logstash logger in your application:

```python
logger = logging.getLogger(__name__)
logger.setLevel(logging.INFO)

logstash_handler = logstash.LogstashHandler('localhost', 5000, version=1)
logger.addHandler(logstash_handler)
```

4. Start logging messages in your code:

```python
logger.info("This is a log message")
```

5. Build and run your Docker container, making sure to include the logstash configuration for the Python application:

```Dockerfile
FROM python:3
COPY . /app
WORKDIR /app
CMD ["python", "your_script.py"]
```

With this setup, the log messages generated in your Python application will be sent to the Logstash service running on localhost and port 5000.

## Conclusion

Integrating Logstash with Docker and Python allows for powerful logging capabilities in your applications. By following the steps outlined in this blog post, you can easily configure Logstash to receive and process log messages from your Python application running in Docker containers. This setup enhances monitoring and debugging by centralizing logs in one location and providing powerful filtering and analysis capabilities.

## References

1. Logstash Documentation: [https://www.elastic.co/guide/en/logstash/current/configuration.html](https://www.elastic.co/guide/en/logstash/current/configuration.html)
2. Python `logstash` Library: [https://github.com/vklochan/python-logstash](https://github.com/vklochan/python-logstash)
3. Docker Official Website: [https://www.docker.com/](https://www.docker.com/)