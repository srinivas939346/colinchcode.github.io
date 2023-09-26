---
layout: post
title: "[python] Server-client communication using Python networking"
description: " "
date: 2023-09-26
tags: [python]
comments: true
share: true
---

In this tutorial, we will explore how to establish a basic server-client communication using Python's networking capabilities. The server will listen for incoming connections from clients, while the clients will connect to the server and send messages.

## Setting up the Server

First, we need to set up our server. Create a new file called `server.py` and add the following code:

```python
import socket

def start_server():
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server_address = ('localhost', 12345)  # Change the IP address and port if needed

    server_socket.bind(server_address)
    server_socket.listen(1)

    print(f"Server listening on {server_address[0]}:{server_address[1]}")

    while True:
        connection, client_address = server_socket.accept()
        print(f"Connection established with {client_address[0]}:{client_address[1]}")

        data = connection.recv(1024).decode()
        print(f"Received: {data}")

        response = "Hello from the server!"
        connection.sendall(response.encode())

        connection.close()

start_server()
```

The code above creates a new socket and binds it to a specific IP address and port (`localhost:12345`). It then listens for incoming connections and accepts them. It receives data from the client, sends a response back, and closes the connection.

## Setting up the Client

Next, let's set up our client. Create another file called `client.py` and add the following code:

```python
import socket

def start_client():
    client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server_address = ('localhost', 12345)  # Change the IP address and port if needed

    client_socket.connect(server_address)

    message = "Hello from the client!"
    client_socket.sendall(message.encode())

    response = client_socket.recv(1024).decode()
    print(f"Received from server: {response}")

    client_socket.close()

start_client()
```

The client code creates a new socket and connects it to the specified server address. It then sends a message to the server and waits for a response. Once the response is received, it prints it out and closes the connection.

## Running the Code

To run the server and client, open two terminals or command prompts. In one terminal, navigate to the directory containing `server.py` and run the following command:

```
python server.py
```

In the other terminal, navigate to the directory containing `client.py` and run the following command:

```
python client.py
```

You should see the server terminal print out the connection details and the received message. The client should print out the response received from the server.

## Conclusion

In this tutorial, you have learned how to establish a basic server-client communication using Python's networking capabilities. This is a fundamental concept in network programming and can be extended to build more complex applications.