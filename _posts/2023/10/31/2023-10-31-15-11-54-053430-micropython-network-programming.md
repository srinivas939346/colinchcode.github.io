---
layout: post
title: "[python] MicroPython network programming"
description: " "
date: 2023-10-31
tags: [python]
comments: true
share: true
---

MicroPython is a lightweight implementation of the Python programming language that is designed to run on microcontrollers and other resource-constrained devices. It provides a subset of the standard Python libraries, along with a few additional modules specific to working with hardware.

In this blog post, we will explore the basics of network programming using MicroPython. We will learn how to connect to a network, send and receive data over TCP/IP, and perform basic HTTP requests.

## Table of Contents
- [Connecting to a Network](#connecting-to-a-network)
- [Sending and Receiving Data](#sending-and-receiving-data)
- [Making HTTP Requests](#making-http-requests)

## Connecting to a Network

MicroPython provides built-in support for connecting to Wi-Fi networks using the `network` module. You can use the following steps to establish a Wi-Fi connection:

1. Import the `network` module:
```python
import network
```

2. Initialize the Wi-Fi interface:
```python
wlan = network.WLAN(network.STA_IF)
```

3. Activate the Wi-Fi interface:
```python
wlan.active(True)
```

4. Connect to a Wi-Fi network using the `connect` method:
```python
wlan.connect("SSID", "password")
```
Replace "SSID" with the name of your Wi-Fi network and "password" with the corresponding password.

Once connected, you can check the IP address assigned to your device by calling the `ifconfig` method:
```python
wlan.ifconfig()
```

## Sending and Receiving Data

Once connected to a network, you can send and receive data over TCP/IP using the `socket` module. Here's an example of how to create a simple TCP client:

1. Import the `socket` module:
```python
import socket
```

2. Create a new socket object:
```python
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
```

3. Connect to a remote server:
```python
s.connect(('remote_server_ip', port))
```
Replace "remote_server_ip" with the IP address of the remote server you want to connect to and "port" with the corresponding port number.

4. Send data to the server using the `send` method:
```python
s.send(b'Hello, server!')
```

5. Receive data from the server using the `recv` method:
```python
data = s.recv(1024)
```

6. Close the connection:
```python
s.close()
```

## Making HTTP Requests

MicroPython provides a simple way to make HTTP requests using the `urequests` module, which is a stripped-down version of the `requests` library. Here's an example of how to make an HTTP GET request:

1. Import the `urequests` module:
```python
import urequests
```

2. Send an HTTP GET request to a URL:
```python
response = urequests.get('http://api.example.com')
```
Replace "http://api.example.com" with the URL you want to send the request to.

3. Get the response content using the `text` attribute:
```python
content = response.text
```

4. Close the request:
```python
response.close()
```

## Conclusion

In this blog post, we learned the basics of network programming using MicroPython. We explored how to connect to a network, send and receive data over TCP/IP, and make HTTP requests. By leveraging the built-in modules provided by MicroPython, you can easily develop network-enabled applications on resource-constrained devices. Happy coding!