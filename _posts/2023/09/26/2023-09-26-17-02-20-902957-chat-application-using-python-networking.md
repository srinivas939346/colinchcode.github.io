---
layout: post
title: "[python] Chat application using Python networking"
description: " "
date: 2023-09-26
tags: [python]
comments: true
share: true
---

In this tutorial, we will walk through the process of creating a simple chat application using Python networking. The application will allow multiple clients to communicate with each other in a real-time chat environment.

## Prerequisites
Before we start, make sure you have Python installed on your machine. You can download and install Python from the official website - [python.org](https://python.org).

## Setting up the Server
We will first create the server-side of our chat application. Open your preferred code editor and create a new Python file, naming it `server.py`. 

In `server.py`, we'll begin by importing the necessary modules: `socket` for networking, `threading` for handling multiple clients, and `sys` for system-related functions.

```python
import socket
import threading
import sys
```

Next, we need to define the server's IP address and port number. We'll use localhost (`'127.0.0.1'`) and an arbitrary port number (`12345`) for this example.

```python
SERVER_HOST = '127.0.0.1'
SERVER_PORT = 12345
```

Now, let's create a `Server` class and define its methods. We'll start by initializing the server socket and setting up the server to listen for client connections.

```python
class Server:
    def __init__(self):
        self.server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        self.server_socket.bind((SERVER_HOST, SERVER_PORT))
        self.server_socket.listen(5)  # Allow up to 5 clients to queue for connection

    def accept_client_connections(self):
        while True:
            client_socket, client_address = self.server_socket.accept()
            print(f'[*] New connection from {client_address}')
            threading.Thread(target=self.handle_client, args=(client_socket,)).start()
```

In the `accept_client_connections` method, we accept client connections and spawn a new thread for each client to handle their messages.

Next, we'll define the `handle_client` method to handle incoming and outgoing client messages.

```python
    def handle_client(self, client_socket):
        while True:
            message = client_socket.recv(1024).decode()
            if not message:
                break
            print(message)
            self.broadcast(message, client_socket)

        client_socket.close()

    def broadcast(self, message, sender_socket):
        for client in clients:
            if client != sender_socket:
                client.send(message.encode())
```

The `handle_client` method receives messages from a client, prints them, and then broadcasts the message to all other connected clients (excluding the sender).

Lastly, let's create an instance of the `Server` class and call the `accept_client_connections` method to start the server.

```python
if __name__ == "__main__":
    server = Server()
    server.accept_client_connections()
```

Save the file and run it by executing `python server.py` in the terminal. Your server is now up and running!

## Creating the Client
To connect to the server and send/receive messages, we'll create the client-side of our chat application. Open a new Python file called `client.py` in your code editor.

In `client.py`, import the necessary modules: `socket`, `threading`, and `sys`.

```python
import socket
import threading
import sys
```

Similar to the server, we need to set up the client's IP address and port number. Update the following variables to match your server's IP and port.

```python
SERVER_HOST = '127.0.0.1'
SERVER_PORT = 12345
```

Now, let's define the `Client` class and its methods. First, create the constructor and set up the client socket.

```python
class Client:
    def __init__(self):
        self.client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        self.client_socket.connect((SERVER_HOST, SERVER_PORT))
```

Next, we'll define the `receive_messages` method to continuously receive messages from the server.

```python
    def receive_messages(self):
        while True:
            try:
                message = self.client_socket.recv(1024).decode()
                print(message)
            except Exception as e:
                print(e)
                self.client_socket.close()
                sys.exit()

    def send_message(self):
        while True:
            message = input()
            self.client_socket.send(message.encode())
```

The `receive_messages` method receives messages from the server and prints them. The `send_message` method allows users to input their messages and send them to the server.

Lastly, create an instance of the `Client` class, call the `receive_messages` method in a new thread, and start sending messages using the `send_message` method.

```python
if __name__ == "__main__":
    client = Client()
    threading.Thread(target=client.receive_messages).start()
    client.send_message()
```

Save the file and run it by executing `python client.py` in the terminal. You can now open multiple instances of the client and start chatting with each other using the server as the mediator.

## Conclusion
Congratulations! You have successfully built a basic chat application using Python networking. Feel free to enhance its functionality by adding features like usernames, private messaging, or file sharing. Happy coding!