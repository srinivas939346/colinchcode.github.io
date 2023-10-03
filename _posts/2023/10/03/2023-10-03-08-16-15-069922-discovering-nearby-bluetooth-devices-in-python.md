---
layout: post
title: "[python] Discovering nearby Bluetooth devices in Python"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

Bluetooth is a wireless communication technology that allows devices to exchange data over short distances. In this article, we will explore how to discover nearby Bluetooth devices using Python.

## Prerequisites

Before we get started, make sure you have the following:

- Python installed on your machine
- Pip package manager installed

## 1. Install the required packages

To interact with Bluetooth devices, we will be using the `pybluez` library. Use the following command to install it:

```python
pip install pybluez
```

## 2. Discovering nearby devices

Now that we have `pybluez` installed, let's write a Python script to discover nearby Bluetooth devices.

```python
import bluetooth

# Discover nearby devices
devices = bluetooth.discover_devices()

# Print the name and address of each device
for device in devices:
    name = bluetooth.lookup_name(device)
    print(f"Device Name: {name}, Address: {device}")
```

In this code, we first import the `bluetooth` module. Then we use the `bluetooth.discover_devices()` method to retrieve a list of all nearby Bluetooth devices. We iterate over this list to get the name and address of each device using the `bluetooth.lookup_name()` function.

## 3. Running the script

Save the script in a file with a `.py` extension, for example, `bluetooth_discovery.py`. Open a terminal or command prompt and navigate to the directory where the file is located. Run the script using the following command:

```bash
python bluetooth_discovery.py
```

You should see the name and address of each nearby Bluetooth device printed on the console.

## Conclusion

In this article, we learned how to discover nearby Bluetooth devices using Python. The `pybluez` library provides a convenient way to interact with Bluetooth devices in your Python projects. This can be useful for various applications, such as building proximity-based systems or IoT solutions.

Make sure to explore the `pybluez` library documentation to discover more functionalities and possibilities.