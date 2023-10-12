---
layout: post
title: "[python] Using callbacks and futures in Asyncio"
description: " "
date: 2023-10-13
tags: [python]
comments: true
share: true
---

In the world of asynchronous programming, `asyncio` is a powerful library in Python that allows you to write concurrent code using coroutines. One of the key features of `asyncio` is its ability to use callbacks and futures to handle asynchronous tasks. In this blog post, we will explore how to use callbacks and futures in `asyncio` to achieve asynchronous execution and ensure efficient concurrency.

## Table of Contents
1. [Callbacks](#callbacks)
2. [Futures](#futures)
3. [Putting it all together](#putting-it-all-together)
4. [Conclusion](#conclusion)

## Callbacks<a name="callbacks"></a>

Callbacks are functions that are passed as arguments to other functions and are called when a specific event or task is completed. In `asyncio`, callbacks can be used to handle the completion of asynchronous tasks. There are two ways to define a callback in `asyncio`:

### Using `asyncio.ensure_future()`

The `asyncio.ensure_future()` function is used to wrap a coroutine or a future object and schedules its execution as soon as possible. It returns a future object that represents the result of the asynchronous task. Here's an example of using `asyncio.ensure_future()` to define a callback:

```python
import asyncio

async def callback_function():
    # Perform some asynchronous task
    await asyncio.sleep(2)
    print("Callback executed")

async def main():
    print("Before callback")
    fut = asyncio.ensure_future(callback_function())
    await asyncio.sleep(1)
    print("After callback")

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
loop.close()
```

In the above example, `callback_function()` is defined as a coroutine function that performs an asynchronous task by sleeping for 2 seconds. The `main()` function is the entry point, where the callback function is wrapped using `asyncio.ensure_future()`. The execution flow is as follows:

1. "Before callback" is printed.
2. `callback_function()` is scheduled to execute, and control is returned to the event loop.
3. `await asyncio.sleep(1)` is used to simulate some other asynchronous work being done while waiting for the callback to complete.
4. "After callback" is printed once the callback function has finished executing.

### Using `asyncio.add_done_callback()`

The `add_done_callback()` method is used to attach a callback function to a future object. The callback function is called when the future's result becomes available or an exception is raised. Here's an example of using `add_done_callback()` to define a callback:

```python
import asyncio

async def callback_function(future):
    # Perform some task
    await asyncio.sleep(2)
    print("Callback executed")

async def main():
    print("Before callback")
    fut = asyncio.Future()
    fut.add_done_callback(callback_function)
    await asyncio.sleep(1)
    fut.set_result(None)
    print("After callback")

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
loop.close()
```

In this example, `callback_function()` is defined as a coroutine function that performs an asynchronous task. The `main()` function is the entry point, where the callback function is attached to a future object using `add_done_callback()`. The execution flow is similar to the previous example.

## Futures<a name="futures"></a>

Futures represent the result of an asynchronous operation and can be used to handle the completion of the operation. In `asyncio`, future objects can be created using `asyncio.ensure_future()` or `asyncio.Future()`. Here's an example of using a future to handle the completion of an asynchronous task:

```python
import asyncio

async def future_example():
    # Perform some asynchronous task
    await asyncio.sleep(2)
    print("Future completed")

async def main():
    fut = asyncio.ensure_future(future_example())
    await fut
    print("After future completion")

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
loop.close()
```

In this example, `future_example()` is defined as a coroutine function that performs an asynchronous task by sleeping for 2 seconds. The `main()` function is the entry point, where the future object is created using `asyncio.ensure_future()`. The `await fut` statement waits for the future object to complete, and once it does, "After future completion" is printed.

## Putting it all together<a name="putting-it-all-together"></a>

Now, let's combine callbacks and futures to create a more complex asynchronous program. Here's an example:

```python
import asyncio

async def callback_function():
    # Perform some asynchronous task
    await asyncio.sleep(2)
    print("Callback executed")

async def main():
    print("Before callback")
    fut = asyncio.ensure_future(callback_function())
    await asyncio.sleep(1)
    print("After callback")

    # Another asynchronous task
    await asyncio.sleep(3)
    print("After another task")

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
loop.close()
```

In this example, we have added another asynchronous task after the callback function. The flow remains the same as before, but now we have introduced additional delays to simulate more work being done asynchronously.

## Conclusion<a name="conclusion"></a>

Using callbacks and futures in `asyncio` enables us to write efficient and concurrent asynchronous code. This blog post has provided an overview of how to use callbacks and futures in `asyncio`. By leveraging these features, you can create robust and responsive applications that make the most of Python's asynchronous programming capabilities.

For more detailed information, you can refer to the official `asyncio` documentation: [Asyncio Documentation](https://docs.python.org/3/library/asyncio.html).