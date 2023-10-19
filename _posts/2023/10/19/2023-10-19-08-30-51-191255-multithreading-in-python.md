---
layout: post
title: "[python] Multithreading in Python"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

Multithreading is a technique in which multiple threads are created and executed concurrently within a single program. 

In Python, threading module provides a way to create and manage threads. This allows developers to execute multiple tasks simultaneously, improving performance and responsiveness of the program.

## Creating a Thread

To create a thread in Python, you need to import the `threading` module and then subclass the `Thread` class. Here's an example:

```python
import threading

class MyThread(threading.Thread):
    def run(self):
        # code to be executed in the thread
        print("Hello from a thread!")

# create an instance of MyThread
thread = MyThread()

# start the thread
thread.start()
```

In the above example, we create a subclass of `Thread` class and define the `run` method. The `run` method contains the code to be executed in the thread. Then, we create an instance of `MyThread` and call the `start` method to start the thread execution.

## Running Multiple Threads

To run multiple threads in Python, you can create multiple instances of your thread subclass and start them. Here's an example:

```python
import threading

class MyThread(threading.Thread):
    def run(self):
        print("Hello from a thread!")

# create multiple instances of MyThread
thread1 = MyThread()
thread2 = MyThread()

# start the threads
thread1.start()
thread2.start()
```

In the above example, we create two instances of `MyThread` and start them using the `start` method. This will execute the code in the `run` method of each thread concurrently.

## Thread Synchronization

When multiple threads access shared resources, synchronization is important to avoid conflicts and ensure proper execution. Python provides synchronization primitives like locks, semaphores, and conditions.

The `Lock` class in the `threading` module can be used to synchronize access to a shared resource. Here's an example:

```python
import threading

shared_variable = 0
lock = threading.Lock()

class MyThread(threading.Thread):
    def run(self):
        global shared_variable
        lock.acquire()
        shared_variable += 1
        lock.release()

# create multiple instances of MyThread
thread1 = MyThread()
thread2 = MyThread()

# start the threads
thread1.start()
thread2.start()

# wait for the threads to finish
thread1.join()
thread2.join()

# print the value of shared_variable
print(shared_variable)
```

In the above example, we use a `Lock` to synchronize access to the `shared_variable`. The `lock.acquire()` method is called before modifying the variable, and the `lock.release()` method is called after modifying it.

## Conclusion

Multithreading allows for concurrent execution of tasks in Python, improving performance and responsiveness. By creating and running multiple threads, developers can take advantage of multi-core processors and perform tasks in parallel. Thread synchronization is crucial to avoid conflicts and ensure proper execution when multiple threads access shared resources.