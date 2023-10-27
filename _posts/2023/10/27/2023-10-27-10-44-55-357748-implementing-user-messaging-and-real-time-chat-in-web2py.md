---
layout: post
title: "[python] Implementing user messaging and real-time chat in Web2py"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Web2py is a powerful web framework written in Python that allows you to easily build web applications. In this tutorial, we will explore how to implement user messaging and real-time chat functionality using Web2py.

## Table of Contents
1. [Setting up the environment](#setting-up-the-environment)
2. [Creating the messaging system](#creating-the-messaging-system)
3. [Enabling real-time chat](#enabling-real-time-chat)
4. [Conclusion](#conclusion)

## Setting up the environment

Before we begin, make sure you have Web2py installed on your machine. You can download it from the official website and follow the installation instructions.

## Creating the messaging system

In order to implement user messaging, we will need a model, a controller, and a view.

### Model

First, let's create a model to define our message table. Open the `models/db.py` file and add the following code:

```python
db.define_table('message',
    Field('sender', 'reference auth_user', default=auth.user_id),
    Field('receiver', 'reference auth_user'),
    Field('content', 'text'),
    Field('timestamp', 'datetime', default=request.now),
    Field('is_read', 'boolean', default=False)
)
```

This model defines a message table with fields for the sender, receiver, content, timestamp, and whether the message has been read or not.

### Controller

Next, let's create a controller to handle the messaging functionality. Create a new file called `controllers/messaging.py` and add the following code:

```python
def index():
    messages = db(db.message.receiver == auth.user_id).select(orderby=~db.message.timestamp)
    return dict(messages=messages)

def send_message():
    form = SQLFORM(db.message)
    if form.process().accepted:
        response.flash = 'Message sent successfully!'
        redirect(URL('index'))
    return dict(form=form)
```

The `index` function retrieves all the messages received by the authenticated user and passes them to the view. The `send_message` function handles the form submission for sending a message.

### View

Now, let's create a view to display the messages and the form to send a new message. Create a new file called `views/messaging/index.html` and add the following code:

```html
{{extend 'layout.html'}}

<h1>Messages</h1>

{{for message in messages:}}
    <div>
        <p>From: {{=message.sender.first_name}} {{=message.sender.last_name}}</p>
        <p>Content: {{=message.content}}</p>
        <p>Timestamp: {{=message.timestamp}}</p>
    </div>
{{pass}}

<h2>Send a new message</h2>

{{=form}}
```

This view displays the list of received messages and provides a form to send a new message.

## Enabling real-time chat

To add real-time chat functionality, we can use Web2py's built-in support for websockets. Let's modify our messaging controller to handle real-time chat.

### Controller

Add the following code to the `controllers/messaging.py` file:

```python
import json

def chat():
    return dict()

def stream():
    def send_message(message):
        response.headers['Content-Type'] = 'application/json'
        response.headers['Cache-Control'] = 'no-cache'
        return json.dumps(message)

    def listen():
        while True:
            message = ws_stream.receive()
            if message:
                message_data = json.loads(message)
                # Process and save the message to the database
                db.message.insert(
                    sender=auth.user_id,
                    receiver=message_data['receiver'],
                    content=message_data['content']
                )
                # Broadcast the message to all connected clients
                ws_stream.send(send_message(message_data))

    if request.env.web2py_action == 'stream':
        response.headers['Content-Type'] = 'application/octet-stream'
        response.headers['Cache-Control'] = 'no-cache'

        if not auth.user:
            raise HTTP(403, 'User not authenticated')

        ws_stream = WebSocket(env, keepalive=5)
        if ws_stream.connection:
            try:
                if request.args(0) == 'listen':
                    listen()
                else:
                    ws_stream.send('Connected')
            except WebSocketError:
                pass
            finally:
                ws_stream.close()
        else:
            raise HTTP(400, 'Websocket connection failed')

```

This code defines a `chat` function to render the chat view and a `stream` function to handle the websocket streaming. The `send_message` function formats the message as JSON, saves it to the database, and broadcasts it to all connected clients.

### View

Create a new file called `views/messaging/chat.html` and add the following code:

```html
{{extend 'layout.html'}}

<h1>Chat</h1>

<div id="messages">
</div>

<form id="chatForm">
    <input type="text" id="receiver" placeholder="Receiver">
    <input type="text" id="content" placeholder="Message">
    <button type="submit">Send</button>
</form>

<script type="text/javascript">
    var ws = new WebSocket("{{=URL('messaging', 'stream', args='listen')}}");

    ws.onmessage = function (event) {
        var message = JSON.parse(event.data);
        var messageElement = document.createElement("p");
        messageElement.innerHTML = "From: " + message.sender + "<br/>Content: " + message.content + "<br/>Timestamp: " + message.timestamp;
        document.getElementById("messages").appendChild(messageElement);
    };

    document.getElementById("chatForm").onsubmit = function (event) {
        event.preventDefault();
        var receiver = document.getElementById("receiver").value;
        var content = document.getElementById("content").value;

        var message = {
            receiver: receiver,
            content: content
        };

        ws.send(JSON.stringify(message));

        document.getElementById("receiver").value = "";
        document.getElementById("content").value = "";
    };
</script>
```

This view displays the chat interface, including the list of messages and the form to send a new message. It establishes a websocket connection and listens for incoming messages. When a message is received, it updates the UI accordingly.

## Conclusion

By following this tutorial, you have learned how to implement user messaging and real-time chat functionality in Web2py. You can now build more interactive and engaging web applications with ease. Happy coding!

## References
- [Web2py official website](https://www.web2py.com/)
- [Web2py GitHub repository](https://github.com/web2py/web2py)