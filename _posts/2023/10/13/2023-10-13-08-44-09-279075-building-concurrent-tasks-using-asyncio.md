---
layout: post
title: "[python] Building concurrent tasks using Asyncio"
description: " "
date: 2023-10-13
tags: [python]
comments: true
share: true
---

In Python, the `Asyncio` framework provides a powerful way to write concurrent code by utilizing asynchronous programming. It allows you to write highly efficient code that can execute multiple tasks concurrently, making it perfect for handling I/O-bound operations.

In this article, we will explore how to build concurrent tasks using `Asyncio` in Python.

## Table of Contents:
1. [Understanding Concurrency](#understanding-concurrency)
2. [What is Asyncio?](#what-is-asyncio)
3. [Creating Concurrent Tasks](#creating-concurrent-tasks)
4. [Handling Asynchronous Operations](#handling-asynchronous-operations)
5. [Synchronization using Locks](#synchronization-using-locks)
6. [Conclusion](#conclusion)

## Understanding Concurrency

Concurrency is the ability to execute multiple tasks simultaneously, allowing them to make progress independently of each other. In traditional programming, this is achieved using threads or processes. However, managing these threads or processes can be complex and error-prone.

## What is Asyncio?

`Asyncio` is a Python library introduced in Python 3.4 that provides a higher-level API for writing asynchronous code. It is built on top of the `async` and `await` keywords introduced in Python 3.5.

With `Asyncio`, you can write asynchronous code using coroutines, which are functions that can be paused and resumed. This allows you to perform I/O-bound operations more efficiently and handle multiple tasks concurrently.

## Creating Concurrent Tasks

To create concurrent tasks with `Asyncio`, you need to define your coroutines using the `async` keyword. You can then execute these coroutines concurrently using an event loop.

Here's an example of creating concurrent tasks using `Asyncio`:

```python
import asyncio

async def task1():
    print("Task 1 started")
    await asyncio.sleep(1)
    print("Task 1 completed")

async def task2():
    print("Task 2 started")
    await asyncio.sleep(2)
    print("Task 2 completed")

async def main():
    await asyncio.gather(task1(), task2())

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
```

In the above code, we define two coroutines `task1` and `task2`. These coroutines simulate some asynchronous operations by pausing using `await asyncio.sleep()`. The `main` coroutine is then created to `gather` and execute the tasks concurrently.

## Handling Asynchronous Operations

`Asyncio` provides various mechanisms to handle asynchronous operations, such as `await`, `asyncio.sleep`, `asyncio.wait`, and `asyncio.as_completed`.

`await` is used to pause the execution of a coroutine until a given asynchronous operation completes. `asyncio.sleep` is used to pause the execution of a coroutine for a specified amount of time.

`asyncio.wait` is used to wait for a group of coroutines to complete. It returns a pair of sets of finished and unfinished tasks.

`asyncio.as_completed` is used to iterate over a collection of coroutines as they complete. It returns an iterator that yields completed tasks as they finish.

## Synchronization using Locks

When working with shared resources, it's important to ensure proper synchronization to avoid race conditions. `Asyncio` provides `Lock` and `Semaphore` objects to synchronize access to shared resources.

A `Lock` can be used to ensure that only one coroutine can access a shared resource at a time. A `Semaphore` can be used to limit the number of coroutines that can access a shared resource simultaneously.

Here's an example of using `Lock` to synchronize access to a shared resource:

```python
import asyncio

async def task(lock):
    print("Task started")
    async with lock:
        print("Accessing shared resource")
        # Do something with the shared resource
    print("Task completed")

async def main():
    lock = asyncio.Lock()
    await asyncio.gather(task(lock), task(lock))

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
```

In the above code, we define the `task` coroutine that uses the `async with` statement to acquire and release the lock. This ensures that only one task can access the shared resource at a time.

## Conclusion

`Asyncio` provides a powerful framework for building concurrent tasks in Python. It simplifies asynchronous programming and allows for efficient execution of I/O-bound operations. By using coroutines, we can write highly concurrent and scalable code. With proper synchronization using locks and semaphores, we can safely access shared resources in our concurrent tasks.

This was just a brief introduction to building concurrent tasks using `Asyncio`. There is a lot more to explore and learn, such as handling exceptions, cancellation, and integrating with other libraries. I encourage you to dive deeper into the `Asyncio` documentation to fully harness its capabilities.

## References:
- [Python Asyncio Documentation](https://docs.python.org/3/library/asyncio.html)
- [Real Python - Async IO in Python: A Complete Walkthrough](https://realpython.com/async-io-python/)