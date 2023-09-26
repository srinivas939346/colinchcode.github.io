---
layout: post
title: "[python] Network packet sniffing with Python"
description: " "
date: 2023-09-26
tags: [python]
comments: true
share: true
---

Packet sniffing is the process of capturing and analyzing network traffic. It allows you to monitor and inspect packets sent over a network, making it a powerful tool for network administrators, security analysts, and developers. In this post, we'll explore how to perform network packet sniffing using Python.

## Prerequisites

Before getting started, let's make sure you have the necessary prerequisites:

- Python installed on your machine.
- `scapy` library installed. You can install it by running `pip install scapy`.

## Capturing Packets

To begin sniffing packets, we'll use the `scapy` library, a popular Python library for packet manipulation. Below is a simple example of capturing and printing network packets:

```python
import scapy.all as scapy

def packet_callback(packet):
    print(packet.summary())

# Start capturing packets on the network interface
scapy.sniff(prn=packet_callback, count=10)
```

In the code snippet above, we import the `scapy` library and define a packet callback function `packet_callback` that simply prints the summary of each captured packet. We then use the `sniff` function to start capturing packets, specifying the packet callback function and the number of packets to capture (in this case, 10).

## Analyzing Packets

Once we have captured the packets, we can perform various analyses on them. For example, we can extract specific information from each packet, such as the source and destination IP addresses. Here's an example of how to analyze packets using `scapy`:

```python
import scapy.all as scapy

def packet_callback(packet):
    if packet.haslayer(scapy.IP):
        src_ip = packet[scapy.IP].src
        dst_ip = packet[scapy.IP].dst
        print(f"Source IP: {src_ip}, Destination IP: {dst_ip}")

scapy.sniff(prn=packet_callback, count=10)
```

In this example, we check if each captured packet has an IP layer (`scapy.IP`). If it does, we extract the source and destination IP addresses using the `src` and `dst` attributes of the IP layer, respectively.

## Advanced Packet Manipulation

Python, along with the `scapy` library, provides advanced capabilities for packet manipulation. You can create your own packets, modify existing ones, and even craft custom network protocols. Here's a simple example of creating and sending a custom TCP packet:

```python
import scapy.all as scapy

packet = scapy.IP(dst="192.168.0.1")/scapy.TCP(dport=80)
scapy.send(packet, verbose=False)
```

In this example, we create a packet that includes an IP layer with a destination IP address of `192.168.0.1` and a TCP layer with a destination port of `80` (the port typically used for HTTP).

## Conclusion

Python, with the help of the `scapy` library, provides a powerful and flexible platform for network packet sniffing. Whether you need to capture and analyze network traffic for troubleshooting, security auditing, or network protocol development, Python can be a valuable tool in your arsenal.

Remember, when working with packet sniffing, always ensure you have the necessary permissions and adhere to legal and ethical guidelines.