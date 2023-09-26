---
layout: post
title: "[python] Port scanning using Python networking"
description: " "
date: 2023-09-26
tags: [python]
comments: true
share: true
---


Port scanning is a technique used to identify open ports on a network or a specific device. Python provides several networking libraries that allow us to perform port scanning easily. In this article, we will explore how to write a simple port scanner using Python.


## Prerequisites

Before we begin, make sure you have Python installed on your system. You can download the latest version of Python from the official Python website: [https://www.python.org/downloads/](https://www.python.org/downloads/)


## Writing the Port Scanner

Let's start by importing the necessary libraries for our port scanner:

```python
import socket
from IPy import IP
```

The `socket` library provides functions that allow us to create network connections, while the `IPy` library allows us to work with IP addresses more conveniently.


Next, we need to define a function that will perform the port scanning:

```python
def scan_port(ip_address, port):
    try:
        sock = socket.socket()
        sock.settimeout(0.5)
        sock.connect((ip_address, port))
        print(f"Port {port} is open")
    except:
        print(f"Port {port} is closed")
```

This function accepts an IP address and a port number as parameters. It creates a socket object and sets a timeout of 0.5 seconds. Then, it tries to establish a connection with the specified IP address and port. If the connection is successful, it prints that the port is open. Otherwise, it prints that the port is closed.


We also need a function to perform the port scan on a range of ports. Let's define another function for that:

```python
def scan(target, ports):
    ip_address = socket.gethostbyname(target)
    print(f"Scanning target: {target}")
    for port in ports:
        scan_port(ip_address, port)
```

This function takes a target hostname or IP address and a list of port numbers as parameters. It uses the `gethostbyname` function from the `socket` library to get the IP address of the target. Then, it iterates over the list of ports and calls the `scan_port` function for each port.


Finally, we need to define the main function where we ask the user for input and perform the port scan:

```python
def main():
    target = input("Enter the target hostname or IP address: ")
    ports = [80, 443, 22, 21, 8080]  # Example ports to scan
    
    scan(target, ports)
```

In the main function, we ask the user to enter the target hostname or IP address. We also define a list of example ports to scan. You can modify this list to include the ports you want to scan.

Once we have all the necessary functions defined, we can call the main function to start the port scanning:

```python
if __name__ == "__main__":
    main()
```

## Conclusion

In this article, we have learned how to write a simple port scanner using Python's networking capabilities. **Port scanning can be useful** for network administrators or security professionals to identify open ports and potential vulnerabilities. Remember to use this knowledge responsibly and only scan networks or devices that you have permission to scan.