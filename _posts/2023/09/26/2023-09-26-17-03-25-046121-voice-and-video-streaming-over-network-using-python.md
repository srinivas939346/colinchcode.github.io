---
layout: post
title: "[python] Voice and video streaming over network using Python"
description: " "
date: 2023-09-26
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to implement voice and video streaming over a network using Python. Streaming audio and video data is becoming increasingly popular with the rise of real-time communication applications. With Python's extensive libraries and frameworks, we can easily build a simple streaming system.

## Prerequisites

To follow along with this tutorial, you will need the following:

- Python 3.x installed on your machine
- Good understanding of Python programming language
- Familiarity with networking concepts

## Dependencies

We will be using the following libraries for our streaming system:

- `OpenCV` - for capturing and processing video frames
- `PyAudio` - for audio capture and playback
- `Socket` - for establishing network connections
- `Struct` - for packing and unpacking binary data

Make sure you have these libraries installed. You can use the `pip` package manager to install them:

```python
pip install opencv-python pyaudio
```

## Setting up the Server

Let's start by creating the server-side script that will handle audio and video streaming.

```python
import socket
import cv2
import pyaudio
import struct
import numpy as np

# Create a socket object
server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Get local machine name
host = socket.gethostname()
port = 5000

# Bind the socket to a specific address and port
server_socket.bind((host, port))

# Listen for incoming connections
server_socket.listen(5)

# Accept connections from clients
client_socket, addr = server_socket.accept()
print("Connection from: ", addr)
```

Here, we create a socket object, bind it to a specific address and port, and listen for incoming connections. Once a connection is made, we accept it and print the client's address.

## Streaming Video

To stream video, we need to capture video frames from the server's camera and send them to the client. Update the server-side script to include the following:

```python
# Create a video capture object
video_capture = cv2.VideoCapture(0)

while True:
    # Read the video frame
    _, frame = video_capture.read()

    # Serialize the frame
    data = cv2.imencode('.jpg', frame)[1].tobytes()

    # Calculate the size of the data
    size = len(data)

    # Send the size of the data to the client
    client_socket.send(struct.pack("L", size))

    # Send the video frame data to the client
    client_socket.sendall(data)

# Release the video capture and close the socket
video_capture.release()
client_socket.close()
```

Here, we capture video frames using `cv2.VideoCapture`, serialize the frames as `.jpg` images, calculate the size of the data, send the size to the client, and finally send the frame data.

## Streaming Audio

For audio streaming, we'll be capturing audio from the server's microphone and sending it to the client. Update the server-side script with the following code:

```python
# Create an audio object
audio = pyaudio.PyAudio()

# Set audio parameters
sample_rate = 44100
chunk_size = 1024

# Open an audio stream
stream = audio.open(format=pyaudio.paInt16, channels=1, rate=sample_rate, input=True, frames_per_buffer=chunk_size)

while True:
    # Read audio data from the stream
    data = stream.read(chunk_size)

    # Send the audio data to the client
    client_socket.sendall(data)

# Close the audio stream and socket
stream.stop_stream()
stream.close()
client_socket.close()
audio.terminate()
```

Here, we create an audio object using `pyaudio.PyAudio`, set the sample rate and chunk size, open an audio stream, read audio data from the stream, and send it to the client.

## Client-side Script

On the client-side, we need to receive the video and audio data and display/play it. Let's create the client-side script:

```python
import socket
import cv2
import pyaudio
import struct
import numpy as np
import threading

# Create a socket object
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Get the server's IP address and port
host = socket.gethostname()
port = 5000

# Connect to the server
client_socket.connect((host, port))

# Create a video capture object
video_capture = cv2.VideoCapture(0)

# Create an audio object
audio = pyaudio.PyAudio()

# Set audio parameters
sample_rate = 44100
chunk_size = 1024

# Open an audio stream
stream = audio.open(format=pyaudio.paInt16, channels=1, rate=sample_rate, output=True, frames_per_buffer=chunk_size)

def receive_video():
    while True:
        # Receive video frame size from the server
        size = struct.unpack("L", client_socket.recv(4))[0]

        if size:
            # Receive video frame data from the server
            data = b""
            while len(data) < size:
                packet = client_socket.recv(size - len(data))
                if not packet:
                    break
                data += packet

            # Convert the received data to an image
            image = cv2.imdecode(np.frombuffer(data, dtype=np.uint8), cv2.IMREAD_COLOR)

            # Display the image
            cv2.imshow("Received Video", image)
            cv2.waitKey(1)

def receive_audio():
    while True:
        # Receive audio data from the server
        data = client_socket.recv(chunk_size)

        if data:
            # Play the audio data
            stream.write(data)

# Start receiving video and audio in separate threads
video_thread = threading.Thread(target=receive_video)
audio_thread = threading.Thread(target=receive_audio)
video_thread.start()
audio_thread.start()

# Wait for threads to finish
video_thread.join()
audio_thread.join()

# Release the video capture and close the socket
video_capture.release()
client_socket.close()
stream.stop_stream()
stream.close()
audio.terminate()
```

On the client-side, we create a socket, connect to the server, create a video capture object, an audio object, and open an audio stream. We also define two functions to receive video and audio data in separate threads. Finally, we start the threads, wait for them to finish, and close the connections.

## Conclusion

In this tutorial, we've learned how to implement voice and video streaming over a network using Python. By leveraging libraries like `OpenCV` and `PyAudio`, we were able to capture, process, and transmit audio and video data between the server and client. This opens up possibilities for building real-time communication applications, video conferencing systems, and more.

Remember to experiment with different options and optimizations to better suit your project's requirements and network conditions.