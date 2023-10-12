---
layout: post
title: "[python] Cancelling and cleaning up tasks in Asyncio"
description: " "
date: 2023-10-13
tags: [python]
comments: true
share: true
---

Asynchronous programming in Python provides a way to execute non-blocking tasks concurrently, which can greatly improve performance in certain scenarios. The `asyncio` module is the built-in library for asynchronous programming in Python. In this blog post, we will focus on how to cancel and clean up tasks in `asyncio`.

### Background

Before we dive into the topic, let's briefly understand the concept of tasks in `asyncio`. A task represents a unit of work that can be executed asynchronously. Tasks are created using the `asyncio.create_task()` function, which takes a coroutine as an argument.

```python
import asyncio

async def my_coroutine():
    # perform some async operations

task = asyncio.create_task(my_coroutine())
```

Once a task is created, it can be scheduled to run by the event loop using `await` or by passing it to `asyncio.ensure_future()`. Tasks can be awaited to wait for their execution to complete.

### Cancelling Tasks

There are cases when you might need to cancel a running task prematurely. This can be useful when you want to stop the execution of a long-running task or to abort an operation due to some external event.

The `task.cancel()` method is used to cancel a task. When a task is cancelled, it raises a `CancelledError` exception inside the coroutine. You can catch this exception and handle it accordingly.

```python
task = asyncio.create_task(my_coroutine())

# ...

task.cancel()
try:
    await task
except asyncio.CancelledError:
    # handle cancellation
    pass
```

It's important to note that cancelling a task only schedules its cancellation. Whether the task actually gets cancelled immediately depends on the nature of the task and the way it handles the cancellation. The underlying coroutine should periodically check for cancellation requests using `asyncio.current_task().cancelled()`, and gracefully exit if a cancellation request has been made.

### Cleaning up Tasks

In addition to cancelling tasks, it's crucial to clean up any resources held by the tasks. For example, if a task is performing file I/O or network operations, you should ensure that any open files or network connections are properly closed when the task is cancelled or completed.

To clean up resources, you can use the `try-finally` construct to ensure that cleanup code is always executed, even if a cancellation or exception occurs.

```python
task = asyncio.create_task(my_coroutine())

try:
    await task
finally:
    # cleanup code here
    pass
```

The code inside the `finally` block will be executed regardless of whether the task completes normally or gets cancelled.

### Conclusion

In this blog post, we learned about cancelling and cleaning up tasks in `asyncio`. We saw how to cancel a running task and how to handle the `CancelledError` exception. We also explored techniques for cleaning up resources held by tasks. Properly managing task cancellation and cleanup is essential for robust asynchronous programming. For more information, refer to the official documentation of `asyncio`.

References:
- [Python asyncio documentation](https://docs.python.org/3/library/asyncio.html)