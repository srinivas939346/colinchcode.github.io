---
layout: post
title: "[python] Bluetooth device discovery using PyBluez library in Python"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

Bluetooth is a wireless technology that enables communication between devices over short distances. The PyBluez library provides a Python interface for accessing Bluetooth functionality on your computer.

In this tutorial, we will learn how to discover nearby Bluetooth devices using the PyBluez library in Python.

## Prerequisites

To follow along with this tutorial, you should have:

- Python installed on your computer.
- The PyBluez library installed. You can install it using pip:
  ```
  pip install pybluez
  ```

## Step 1: Import the necessary modules

First, let's import the necessary modules from PyBluez:

```python
import bluetooth
```

## Step 2: Discover nearby devices

To discover nearby Bluetooth devices, we can use the `discover_devices()` function from the `bluetooth` module. This function returns a list of discovered device addresses.

```python
devices = bluetooth.discover_devices()
```

## Step 3: Print discovered device information

Once we have the list of discovered devices, we can iterate over it and print information about each device. The `lookup_name()` function can be used to retrieve the friendly name of a device using its address.

```python
for device in devices:
    name = bluetooth.lookup_name(device)
    print(f"Device: {name}, Address: {device}")
```

## Step 4: Run the script

Save the script with a .py extension, and run it from the command line:

```
python bluetooth_discovery.py
```

The script will start scanning for nearby Bluetooth devices and print their friendly name and address.

## Conclusion

In this tutorial, we learned how to discover nearby Bluetooth devices using the PyBluez library in Python. You can now use this knowledge to build more advanced applications involving Bluetooth communication. Happy coding!