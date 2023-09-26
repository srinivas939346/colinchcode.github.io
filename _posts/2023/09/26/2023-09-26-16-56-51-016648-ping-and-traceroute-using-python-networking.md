---
layout: post
title: "[python] Ping and traceroute using Python networking"
description: " "
date: 2023-09-26
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to implement ping and traceroute functionality using Python's networking libraries. These utilities are commonly used in network troubleshooting and diagnostics to test the reachability and latency of a remote host. 

Let's get started!

## Ping

Ping is a network diagnostic tool that sends an ICMP Echo Request to a remote host and waits for an ICMP Echo Reply. It measures the round-trip time (RTT) between the sender and receiver. The `ping` command is available on most operating systems, but we can also implement it in Python.

Here's a simple Python code snippet that uses the `ping` library to ping a remote host.

```python
import ping3

def ping_host(host):
    try:
        response_time = ping3.ping(host)
        if response_time is not None:
            print(f"Ping successful! Response time: {response_time} ms")
        else:
            print("Ping failed!")
    except Exception as e:
        print(f"Ping failed! Error: {str(e)}")

ping_host("www.google.com")
```

In the above code, we import the `ping3` library and define a function `ping_host` that accepts the hostname or IP address as a parameter. We use the `ping` function from the `ping3` library to send an ICMP Echo Request to the specified host. If a response is received, we print the response time. Otherwise, we print a failure message.

## Traceroute

Traceroute is another network diagnostic tool that traces the route packets take from your computer to a destination IP address or hostname. It provides valuable information about the number of hops, IP addresses, and round-trip times taken by packets to reach the destination. Similar to the `ping` command, we can also implement traceroute in Python.

For implementing traceroute in Python, we will use the `scapy` library. Scapy is a powerful packet manipulation library that allows us to create, send, capture, and analyze network packets. Here's an example code snippet to perform traceroute using `scapy`.

```python
from scapy.all import *

def traceroute_host(host):
    ttl = 1
    while True:
        pckt = IP(dst=host, ttl=ttl) / ICMP()
        reply = sr1(pckt, verbose=False, timeout=1)
        if reply is None:
            break
        elif reply.type == 11:
            print(f"ttl={ttl} {reply.src}")
        elif reply.type == 0:
            print(f"ttl={ttl} {reply.src} - Reached Destination!")
            break
        else:
            print(f"ttl={ttl} *")

        ttl += 1

traceroute_host("www.google.com")
```

In the above code, we import the `scapy` library and define a function `traceroute_host` that accepts the hostname or IP address as a parameter. We repeatedly send ICMP packets with increasing time-to-live (TTL) values. Whenever we receive a time exceeded ICMP reply (type 11), we print the intermediate hop IP address along with the corresponding TTL value. When we receive an ICMP reply with type 0 (Echo Reply), it means that we have reached the destination.

## Conclusion

Ping and traceroute are essential tools in network troubleshooting and diagnostics. With Python, we can implement these functionalities using various libraries like `ping3` and `scapy`. By incorporating these functionalities into our own scripts or applications, we can perform network measurements and identify network issues more efficiently.

I hope you found this blog post useful!