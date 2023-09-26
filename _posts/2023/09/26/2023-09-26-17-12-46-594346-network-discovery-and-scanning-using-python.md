---
layout: post
title: "[python] Network discovery and scanning using Python"
description: " "
date: 2023-09-26
tags: [python]
comments: true
share: true
---

Network discovery and scanning are essential tasks for network administrators and security professionals to ensure the security and smooth operation of their networks. Python, as a versatile and powerful programming language, provides several libraries and tools that make it easy to implement network discovery and scanning functionalities.

In this blog post, we will explore some of the popular Python libraries and demonstrate how to use them for network discovery and scanning purposes.

## 1. `Scapy` Library

[Scapy](https://scapy.net/) is a powerful Python library for network discovery, packet manipulation, and network scanning. It allows you to craft, send, receive, and analyze network packets programmatically.

With Scapy, you can perform a wide range of network scanning activities, such as host discovery, port scanning, and operating system fingerprinting. Here's an example of how to perform a basic host discovery using Scapy:

```python
from scapy.all import srp, Ether, ARP

def discover_hosts(interface):
    broadcast = "ff:ff:ff:ff:ff:ff"
    ether_layer = Ether(dst=broadcast)
    arp_layer = ARP(pdst="192.168.0.0/24")
    packet = ether_layer / arp_layer

    answered, unanswered = srp(packet, iface=interface, timeout=2, verbose=False)

    for send_packet, received_packet in answered:
        print(received_packet.psrc, received_packet.hwsrc)


discover_hosts("eth0")
```

In the above example, we use the `srp()` function from Scapy to send and receive packets. We craft an Ethernet layer and an ARP layer to send an ARP request to discover the hosts on the network. The results are then printed to the console.

## 2. `Nmap` Module

[Nmap](https://pypi.org/project/python-nmap/) is a popular open-source tool used for network exploration and security auditing. It provides a Python module called `python-nmap` that allows you to interact with Nmap and perform network scanning tasks programmatically.

To use `python-nmap`, you need to have Nmap installed on your system. Here's an example of using `python-nmap` to scan for open ports on a host:

```python
import nmap

def scan_open_ports(target):
    scanner = nmap.PortScanner()
    scanner.scan(target, arguments="-p 1-1000")

    for host in scanner.all_hosts():
        for port in scanner[host]["tcp"]:
            if scanner[host]["tcp"][port]["state"] == "open":
                print(f"Port {port} is open on {host}")


scan_open_ports("192.168.0.1")
```

In the example above, we create a `PortScanner` object from `nmap` and use the `scan()` method to scan the specified target for open TCP ports. We then iterate over the results and print the open ports.

## Conclusion

Python provides powerful libraries and tools for network discovery and scanning. In this blog post, we explored the `Scapy` library for packet manipulation and network scanning, as well as the `python-nmap` module for interacting with Nmap.

These are just two examples of the many tools available in Python for network discovery and scanning. Depending on your specific requirements, you can choose the most suitable library or tool to ensure the security and efficiency of your network.