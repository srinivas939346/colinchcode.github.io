---
layout: post
title: "[python] IPv4 and IPv6 address manipulation using Python"
description: " "
date: 2023-09-26
tags: [python]
comments: true
share: true
---

Handling IPv4 and IPv6 addresses is a common task in networking and application development. Python provides several libraries and built-in modules to manipulate and work with IP addresses. In this tutorial, we will explore how to manipulate IPv4 and IPv6 addresses using Python.

## IPv4 Address Manipulation

Python's `ipaddress` module provides classes for working with IPv4 and IPv6 addresses. To manipulate IPv4 addresses, we can make use of the `IPv4Address` class from the `ipaddress` module. Here's an example of how to manipulate IPv4 addresses:

```python
import ipaddress

# Create an IPv4 address object
ip = ipaddress.IPv4Address('192.168.0.1')

# Access properties of the IPv4 address
print("IP:", ip)
print("IP version:", ip.version)

# Check if the IP address is private
print("Is private:", ip.is_private)

# Get the network address and the hostmask
network_address = ip.network
hostmask = ip.hostmask

print("Network address:", network_address)
print("Hostmask:", hostmask)

# Perform arithmetic operations
ip += 1
print("Next IP:", ip)

ip -= 1
print("Previous IP:", ip)

# Check if two IP addresses are in the same network
other_ip = ipaddress.IPv4Address('192.168.0.5')
print("Are in the same network:", ip in ipaddress.IPv4Network('192.168.0.0/24'))
print("Are in the same network:", other_ip in ipaddress.IPv4Network('192.168.0.0/24'))
```

In the above example, we created an `IPv4Address` object using the IP address '192.168.0.1'. We then accessed various properties such as the IP version and whether it is a private IP address. We also performed arithmetic operations like incrementing and decrementing the IP address.

We can also check if two IP addresses are in the same network using the `in` operator, as shown in the last few lines of the code.

## IPv6 Address Manipulation

Python's `ipaddress` module also provides classes for working with IPv6 addresses. To manipulate IPv6 addresses, we can make use of the `IPv6Address` class from the `ipaddress` module. Here's an example of how to manipulate IPv6 addresses:

```python
import ipaddress

# Create an IPv6 address object
ip = ipaddress.IPv6Address('2001:db8::1')

# Access properties of the IPv6 address
print("IP:", ip)
print("IP version:", ip.version)

# Get the network address and the hostmask
network_address = ip.network
hostmask = ip.hostmask

print("Network address:", network_address)
print("Hostmask:", hostmask)

# Perform arithmetic operations
ip += 1
print("Next IP:", ip)

ip -= 1
print("Previous IP:", ip)

# Check if two IP addresses are in the same network
other_ip = ipaddress.IPv6Address('2001:db8::2')
print("Are in the same network:", ip in ipaddress.IPv6Network('2001:db8::/64'))
print("Are in the same network:", other_ip in ipaddress.IPv6Network('2001:db8::/64'))
```

In the above example, we created an `IPv6Address` object using the IP address '2001:db8::1'. We then accessed various properties such as the IP version and performed arithmetic operations similar to IPv4 addresses. We also checked if two IP addresses are in the same network using the `in` operator.

By utilizing the `ipaddress` module, we can easily manipulate and perform operations on IPv4 and IPv6 addresses in Python. This makes it convenient for tasks such as validating, calculating subnets, and more.

In conclusion, Python provides powerful libraries and modules like `ipaddress` for working with IPv4 and IPv6 addresses. Whether it's manipulating or validating IP addresses, Python has got us covered.