---
layout: post
title: "[python] Bluetooth low energy (BLE) communication in Python"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

Bluetooth Low Energy (BLE) is a wireless communication technology designed for short-range communication between devices. It is commonly used in applications such as fitness trackers, smartwatches, and home automation devices. In this blog post, we will explore how to establish a BLE communication in Python.

## Prerequisites

To follow this tutorial, you will need the following:

- A device with Bluetooth Low Energy support
- Python 3.x installed on your computer
- The `pybluez` library installed (`pip install pybluez`)

## Scanning for BLE Devices

To start with BLE communication, we first need to scan for nearby BLE devices. The `pybluez` library provides a simple way to scan for BLE devices in Python. Here's a simple script to scan for devices:

```python
import bluetooth

devices = bluetooth.discover_devices(duration=10, lookup_names=True)

for addr, name in devices:
    print(f"Found device: {name} ({addr})")
```

This script uses the `bluetooth.discover_devices()` function to scan for devices. It returns a list of tuples containing the device address and name. The `duration` argument specifies the scanning duration in seconds.

## Connecting to a BLE Device

Once we have identified a BLE device, we can establish a connection to it. Typically, a BLE device offers one or more services that provide access to specific functionalities. We can connect to a specific service using its UUID (Universally Unique Identifier). Here's an example of how to connect to a BLE device and discover its available services:

```python
import bluetooth

# Replace with the device address you want to connect to
device_address = "00:11:22:33:AA:BB"

services = bluetooth.find_service(address=device_address)

for service in services:
    print(f"Service Name: {service['name']}")
    print(f"Service Description: {service['description']}")
    print(f"Service Protocol: {service['protocol']}")
    print(f"Service Provider: {service['provider']}\n")
```

In this script, we use the `bluetooth.find_service()` function to find services available on the specified device. It returns a list of dictionaries, each containing information about a service.

## Interacting with a BLE Service

Once we have connected to a BLE device and discovered its services, we can interact with a specific service using its UUID. Depending on the service, you may need to read or write data, or even subscribe to notifications. The specific details for each service depend on the device and its documentation.

Here's an example of how to read data from a specific BLE characteristic:

```python
import bluetooth

# Replace with the device address and characteristic UUID you want to interact with
device_address = "00:11:22:33:AA:BB"
characteristic_uuid = "0000FFFF-0000-1000-8000-00805F9B34FB"

sock = bluetooth.BluetoothSocket(bluetooth.RFCOMM)
sock.connect((device_address, bluetooth.PORT_ANY))

sock.send(bytes.fromhex("01"))

data = sock.recv(1024)
print(f"Received data: {data.decode()}")

sock.close()
```

In this script, we establish a Bluetooth socket connection to the device using the `bluetooth.BluetoothSocket()` class. We send a command to the device and receive its response.

## Conclusion

Python provides convenient libraries like `pybluez` to facilitate BLE communication. In this blog post, we explored how to scan for BLE devices, connect to a specific device and service, and interact with its characteristics. You can use this knowledge as a starting point to build your own BLE applications in Python.

Remember to import the necessary modules and libraries, and ensure that your device has the required Bluetooth Low Energy capabilities. Happy Bluetooth coding!