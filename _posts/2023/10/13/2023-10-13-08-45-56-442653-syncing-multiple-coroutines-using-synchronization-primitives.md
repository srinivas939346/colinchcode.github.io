---
layout: post
title: "[python] Syncing multiple coroutines using synchronization primitives"
description: " "
date: 2023-10-13
tags: [python]
comments: true
share: true
---

When working with asynchronous programming in Python, you might come across scenarios where you need to synchronize multiple coroutines to ensure they execute in a specific order or wait for each other's completion. Thankfully, Python provides various synchronization primitives that can help achieve this synchronization. In this blog post, we will explore some of these synchronization primitives and how they can be used to synchronize multiple coroutines.

## Table of Contents
- [Introduction](#introduction)
- [The `asyncio.Event` Primitive](#event-primitive)
- [The `asyncio.Lock` Primitive](#lock-primitive)
- [The `asyncio.Semaphore` Primitive](#semaphore-primitive)
- [The `asyncio.Condition` Primitive](#condition-primitive)
- [Conclusion](#conclusion)

## Introduction <a name="introduction"></a>

Asynchronous programming in Python is based on the `asyncio` library, which introduces the concept of coroutines. Coroutines are lightweight units of execution that can be scheduled independently and suspended/resumed during execution, allowing for efficient asynchronous programming. However, when working with multiple coroutines, it becomes essential to synchronize their execution to avoid race conditions and ensure proper coordination.

## The `asyncio.Event` Primitive <a name="event-primitive"></a>

The `asyncio.Event` is a simple synchronization primitive that allows coroutines to wait until a particular event occurs. It has two main methods: `wait()` and `set()`. `wait()` suspends the execution until the event is set, while `set()` triggers the event and resumes the waiting coroutines.

```python
import asyncio

async def coroutine_1(event):
    print("Coroutine 1 is waiting...")
    await event.wait()
    print("Coroutine 1 resumed.")

async def coroutine_2(event):
    print("Coroutine 2 is doing some work...")
    await asyncio.sleep(2)
    event.set()
    print("Coroutine 2 finished its work.")

async def main():
    event = asyncio.Event()
    await asyncio.gather(coroutine_1(event), coroutine_2(event))

asyncio.run(main())
```

In the above example, `coroutine_1` waits for `coroutine_2` to set the event before resuming its execution. The `wait()` method suspends the coroutine until the event is set by `coroutine_2` using `set()`.

## The `asyncio.Lock` Primitive <a name="lock-primitive"></a>

The `asyncio.Lock` primitive provides a simple way to enforce exclusive access to a shared resource among multiple coroutines. It has two methods: `acquire()` and `release()`. `acquire()` blocks coroutines until the lock is acquired, while `release()` releases the lock.

```python
import asyncio

async def coroutine(lock):
    print("Coroutine trying to acquire the lock...")
    async with lock:
        print("Lock acquired.")
        await asyncio.sleep(2)
    print("Lock released.")

async def main():
    lock = asyncio.Lock()
    await asyncio.gather(coroutine(lock), coroutine(lock))

asyncio.run(main())
```

In the example above, both coroutines attempt to acquire the lock using `async with lock`. Only one coroutine can acquire the lock at a time, guaranteeing exclusive access to the critical section within the context block.

## The `asyncio.Semaphore` Primitive <a name="semaphore-primitive"></a>

The `asyncio.Semaphore` primitive is used to limit the number of coroutines that can access a resource simultaneously. It provides two methods: `acquire()` and `release()`. `acquire()` blocks coroutines until the semaphore is available, while `release()` increments the semaphore count.

```python
import asyncio

async def coroutine(semaphore):
    await semaphore.acquire()
    print("Acquired semaphore.")
    await asyncio.sleep(2)
    semaphore.release()
    print("Released semaphore.")

async def main():
    semaphore = asyncio.Semaphore(1)
    await asyncio.gather(coroutine(semaphore), coroutine(semaphore))

asyncio.run(main())
```

In this example, only one coroutine can acquire the semaphore at a time due to the `Semaphore(1)` initialization. The second coroutine needs to wait until the semaphore is released by the first coroutine.

## The `asyncio.Condition` Primitive <a name="condition-primitive"></a>

The `asyncio.Condition` primitive is a more complex synchronization primitive that allows coroutines to synchronize their execution based on specific conditions. It provides methods like `wait()`, `notify()`, and `notify_all()`.

```python
import asyncio

async def producer(condition):
    async with condition:
        print("Producer putting an item...")
        await asyncio.sleep(2)
        condition.notify()

async def consumer(condition):
    async with condition:
        print("Consumer waiting for an item...")
        await condition.wait()
        print("Consumer received an item.")

async def main():
    condition = asyncio.Condition()
    await asyncio.gather(producer(condition), consumer(condition))

asyncio.run(main())
```

The `producer` and `consumer` coroutines use the `Condition` primitive to synchronize their execution. The `producer` puts an item and calls `condition.notify()`, while the `consumer` waits for an item using `condition.wait()`.

## Conclusion <a name="conclusion"></a>

Synchronizing multiple coroutines in Python is essential for proper coordination and avoiding race conditions. The `asyncio` library provides several synchronization primitives like `Event`, `Lock`, `Semaphore`, and `Condition` that help in achieving this synchronization. Understanding these primitives and their usage will enable you to write robust and efficient asynchronous code.

References:
- [Python asyncio documentation](https://docs.python.org/3/library/asyncio.html)
- [Real Python - Async IO in Python: A Complete Walkthrough](https://realpython.com/async-io-python/)
- [Towards Data Science - Asynchronous Programming in Python with Asyncio](https://towardsdatascience.com/asynchronous-programming-in-python-with-asyncio-b0dc34Bf1ac)

*Note: The code examples provided in this blog post assume the usage of Python 3.7 or newer.*