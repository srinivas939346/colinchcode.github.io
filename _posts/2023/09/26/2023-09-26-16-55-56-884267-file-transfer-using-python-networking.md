---
layout: post
title: "[python] File transfer using Python networking"
description: " "
date: 2023-09-26
tags: [python]
comments: true
share: true
---

File transfer is a common requirement in many networking applications. In this blog post, we will explore how to use Python's networking capabilities to transfer files between a server and a client.

## Setting up the Server

First, let's set up the server that will receive the file. Here's an example of how you can create a simple file server using Python's `socket` module:

```python
import socket

def start_server():
    host = '127.0.0.1'
    port = 12345
    
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server_socket.bind((host, port))
    server_socket.listen(1)
    
    print(f"Server listening on {host}:{port}")
    
    while True:
        conn, addr = server_socket.accept()
        
        with open('received_file.txt', 'wb') as file:
            while True:
                data = conn.recv(1024)
                
                if not data:
                    break
                
                file.write(data)
                
        conn.close()
        print("File received successfully.")

if __name__ == '__main__':
    start_server()
```

In the above code, we create a TCP server socket and bind it to a specific host and port. We then listen for incoming connections. Once a client connects, we open a file in write binary mode to receive the transferred file. The received data is written to the file until the transfer is complete. The connection is closed after the file is received.

## Transferring the File from Client

Now let's see how to transfer a file from a client to the server using Python's `socket` module:

```python
import socket

def send_file():
    host = '127.0.0.1'
    port = 12345
    
    client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    client_socket.connect((host, port))
    
    file_path = 'file_to_send.txt'
    
    with open(file_path, 'rb') as file:
        data = file.read(1024)
        
        while data:
            client_socket.send(data)
            data = file.read(1024)
    
    client_socket.close()
    print("File sent successfully.")

if __name__ == '__main__':
    send_file()
```

In the above code, we create a TCP client socket and connect it to the server's host and port. We then read the file in chunks of 1024 bytes and send each chunk over the socket until the entire file is transferred. Finally, we close the socket and print a success message.

## Conclusion

Python's networking capabilities make it easy to transfer files between a server and a client. You can use the `socket` module to create a server that listens for incoming connections and receives files. Similarly, you can create a client that connects to the server and sends files. This can be useful in scenarios such as uploading files to a server or sharing files between devices on a local network.

Keep in mind that these are simplified examples and may not handle all error and edge cases. It's important to add error handling and additional functionality depending on your specific use case.