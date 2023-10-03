---
layout: post
title: "[python] Bluetooth device pairing using PyBluez library in Python"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

Bluetooth is a widely used wireless technology that allows devices to communicate with each other over short distances. In Python, the PyBluez library provides a simple interface to perform various Bluetooth-related operations. In this tutorial, we will explore how to pair a Bluetooth device using PyBluez in Python.

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Installing PyBluez](#installing-pybluez)
3. [Detect available Bluetooth devices](#detect-available-devices)
4. [Pairing a Bluetooth device](#pairing-a-device)
5. [Conclusion](#conclusion)

## Prerequisites <a name="prerequisites"></a>
Before we proceed, make sure you have the following:

- Python installed on your system
- PyBluez library installed (we will cover the installation process in the next section)
- A Bluetooth device that you want to pair with your system

## Installing PyBluez <a name="installing-pybluez"></a>
To install PyBluez, open your terminal or command prompt and run the following command:

```bash
pip install pybluez
```

This will download and install the PyBluez library along with any required dependencies.

## Detect available Bluetooth devices <a name="detect-available-devices"></a>
Before we can pair a Bluetooth device, we need to detect the available devices in range. We can achieve this using the following code:

```python
import bluetooth

def detect_devices():
    devices = bluetooth.discover_devices()
    for addr in devices:
        print("Device:", bluetooth.lookup_name(addr), " Address:", addr)

detect_devices()
```

In the above code, we import the `bluetooth` module and use the `discover_devices` function to obtain a list of Bluetooth device addresses within range. We then iterate over each address and print the device name along with its address.

## Pairing a Bluetooth device <a name="pairing-a-device"></a>
To pair a Bluetooth device, we need to use the `bluetooth` module's `pair` function. Here's an example:

```python
import bluetooth

def pair_device(device_address):
    result = bluetooth.pair(device_address)
    if result == bluetooth.CONN_SUCCESS:
        print("Device paired successfully.")
    else:
        print("Pairing failed.")

pair_device('00:11:22:33:44:55')  # Replace with the Bluetooth device address you want to pair
```

In the above code, we define a `pair_device` function that takes the device address as an argument. We then call the `pair` function with the device address, and if the pairing is successful, we print a success message; otherwise, we print a failure message.

Make sure to replace `'00:11:22:33:44:55'` with the actual Bluetooth device address you want to pair.

## Conclusion <a name="conclusion"></a>
Pairing a Bluetooth device using PyBluez in Python is a straightforward task. We first detect the available devices using the `discover_devices` function, and then use the `pair` function to pair a specific device. With PyBluez, you can build powerful Bluetooth applications in Python.