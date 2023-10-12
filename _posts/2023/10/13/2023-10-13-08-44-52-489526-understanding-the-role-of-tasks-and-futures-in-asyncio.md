---
layout: post
title: "[python] Understanding the role of tasks and futures in Asyncio"
description: " "
date: 2023-10-13
tags: [python]
comments: true
share: true
---

Asynchronous programming has become increasingly important in modern software development, as it allows programs to efficiently handle concurrency and improve performance. In Python, Asyncio is a powerful framework that provides a convenient way to write asynchronous code.

## What are tasks and futures?

Tasks and futures are two fundamental components in the Asyncio framework. These components are used to manage concurrency and handle asynchronous operations.

**Tasks**: A task is a high-level construct that represents a coroutine running in the Asyncio event loop. In other words, it is a unit of work that can be scheduled and managed by the event loop. Tasks are created by calling the `asyncio.create_task()` function, which takes a coroutine object as an argument.

**Futures**: A future is a low-level construct that represents the result of an asynchronous operation. It is similar to a promise in other programming languages. A future is created when a task is scheduled and is used to retrieve the result of the task once it completes. 

## How tasks and futures work together

Tasks and futures work together to enable asynchronous programming in Python. When a task is created using `asyncio.create_task()`, a future is also created internally to represent the result of the task. The future object is returned by the `create_task()` function and can be used to retrieve the result of the task.

Tasks are scheduled to run in the event loop, and once a task completes, the future associated with it is marked as done. The result of the task can be obtained by calling the `result()` method on the future object. This method will block until the task completes and returns the result.

Additionally, futures provide other methods to check the status of the underlying task, and to add callbacks or await their completion using the `add_done_callback()` and `await` syntax respectively.

## Example Usage

```python
import asyncio

async def my_async_function():
    # perform some asynchronous operations
    await asyncio.sleep(1)
    return "Async task completed"

async def main():
    task = asyncio.create_task(my_async_function())
    print("Task created")

    await asyncio.sleep(0.5)

    if task.done():
        result = task.result()
        print(f"Task result: {result}")

asyncio.run(main())
```

In the example above, we have a simple `my_async_function()` that performs an asynchronous task of waiting for 1 second and then returning a string. We create a task by calling `asyncio.create_task()` with the coroutine object as an argument. After a short delay, we check if the task is done using `task.done()` and retrieve the result using `task.result()`.

## Conclusion

Tasks and futures are important components in the Asyncio framework that enable asynchronous programming in Python. They provide a way to manage concurrency and handle asynchronous operations efficiently. By understanding how tasks and futures work together, you can write more effective and responsive asynchronous code in your Python projects.

**References:**
- [Asyncio - Tasks and Coroutines](https://docs.python.org/3/library/asyncio-task.html)
- [Asyncio - Futures](https://docs.python.org/3/library/asyncio-future.html)