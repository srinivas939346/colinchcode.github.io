---
layout: post
title: "[python] Building a simple network server using Asyncio"
description: " "
date: 2023-10-13
tags: [python]
comments: true
share: true
---

In this tutorial, we will explore how to build a simple network server using the Asyncio module in Python. Asyncio is a powerful library that allows you to write concurrent code using coroutines, multiplexing I/O access over sockets and other resources, running network clients and servers, and other related primitives.

## Table of Contents
1. [Introduction to Asyncio](#introduction-to-asyncio)
2. [Setting up the Server](#setting-up-the-server)
3. [Creating a Basic Server](#creating-a-basic-server)
4. [Handling Client Connections](#handling-client-connections)
5. [Conclusion](#conclusion)

## Introduction to Asyncio
Asyncio is a library for writing single-threaded concurrent code using coroutines, multiplexing I/O access over sockets, and other resources. It is designed to be fast and scalable, making it ideal for building high-performance network servers.

## Setting up the Server
Before we start building our server, let's make sure we have the Asyncio library installed. You can install it by running the following command:

```python
pip install asyncio
```

Once the library is installed, we can start building our server.

## Creating a Basic Server
The first step in building our server is to import the necessary modules and create an event loop.

```python
import asyncio

async def handle_client(reader, writer):
    # Code to handle client requests
    
async def start_server():
    server = await asyncio.start_server(
        handle_client, 'localhost', 8888)
    async with server:
        await server.serve_forever()

asyncio.run(start_server())
```

In the above code, we define an `async` function called `handle_client()`, which takes in a reader and a writer as arguments. This function will be responsible for handling client requests.

We then define another `async` function called `start_server()`, which creates the server using the `asyncio.start_server()` function. In this example, we specify `'localhost'` as the hostname and `8888` as the port number.

Finally, we run the `start_server()` function using `asyncio.run()`.

## Handling Client Connections
Now that we have our basic server set up, let's add some code to handle client connections. In the `handle_client()` function, we can add logic to read and write data to the client.

```python
import asyncio

async def handle_client(reader, writer):
    data = await reader.read(100)
    message = data.decode()
    print(f'Received: {message}')

    response = 'Hello from the server!'
    writer.write(response.encode())
    await writer.drain()

    print('Closing the connection')
    writer.close()

async def start_server():
    server = await asyncio.start_server(
        handle_client, 'localhost', 8888)
    async with server:
        await server.serve_forever()

asyncio.run(start_server())
```

In the updated code, we use the `reader.read()` function to read data from the client socket. We then decode the received data using `.decode()` and print the message.

Next, we define a response message and use `writer.write()` to send the response to the client. We also use `await writer.drain()` to ensure that the data is sent before proceeding.

Finally, we close the connection with the client using `writer.close()`.

## Conclusion
In this tutorial, we have seen how to build a simple network server using the Asyncio module in Python. We learned about the basics of Asyncio and how to handle client connections. Asyncio provides a powerful and efficient way to write concurrent code, making it essential for building network servers that can handle multiple client connections simultaneously.