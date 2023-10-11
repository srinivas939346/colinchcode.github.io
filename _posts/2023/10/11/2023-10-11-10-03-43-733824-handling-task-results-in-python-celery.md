---
layout: post
title: "[python] Handling task results in Python Celery"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

Celery is a distributed task queue library written in Python. It allows you to distribute and run tasks asynchronously across multiple worker nodes. One important aspect of working with Celery is handling the results of the tasks that are executed.

In this article, we will explore different ways to handle task results in Python Celery.

## Table of Contents
- [Synchronous Task Execution](#synchronous-task-execution)
- [Asynchronous Task Execution](#asynchronous-task-execution)
- [Handling Task Results](#handling-task-results)
    - [Using AsyncResult Object](#using-asyncresult-object)
    - [Using Callbacks](#using-callbacks)
    - [Using Chains](#using-chains)
- [Conclusion](#conclusion)

## Synchronous Task Execution

By default, Celery executes tasks synchronously. This means that the call to a task will block until the task finishes executing. In this case, handling the task result is straightforward as we get the return value directly.

```python
from celery import Celery

app = Celery('demo', backend='rpc://', broker='pyamqp://')

@app.task
def add(x, y):
    return x + y

result = add.delay(5, 10)
print(result.get())  # 15
```

In the above example, `add.delay(5, 10)` schedules the task for execution and returns a `AsyncResult` object. The `result.get()` method is used to fetch the result of the task.

## Asynchronous Task Execution

Celery also provides the option to execute tasks asynchronously, allowing multiple tasks to run concurrently. To enable asynchronous execution, you need to configure a message broker and result backend.

```python
app = Celery('demo', backend='rpc://', broker='pyamqp://')
```

With asynchronous execution, the result is not immediately available. Therefore, we need to implement some mechanism to handle the task results.

## Handling Task Results

### Using AsyncResult Object

To handle task results in Celery, you can use the `AsyncResult` object returned by the `delay()` method. This object provides various methods to monitor and fetch the task result.

```python
result = add.delay(5, 10)

# Check if the task is complete
print(result.ready())  # False

# Wait for the task to complete
result.wait()

# Check again
print(result.ready())  # True

# Get the task result
print(result.result)  # 15
```

The `ready()` method checks whether the task has completed, while `wait()` is used to block until the task finishes. Finally, the `result` attribute provides the actual result of the task.

### Using Callbacks

Celery also allows you to attach callbacks to execute when the task finishes. This can be useful in scenarios where you want to perform additional actions based on the task result.

```python
def handle_result(task_result):
    # Process task result
    print(task_result)

result = add.apply_async((5, 10))
result.then(handle_result)
```

In the above example, the `handle_result` function is defined to handle the task result. The `then()` method is used to attach the callback to the task.

### Using Chains

Celery provides a `Chain` object that allows you to chain multiple tasks together, where each task depends on the result of the previous task.

```python
from celery import chain

@app.task
def multiply(x, y):
    return x * y

result = chain(add.s(5, 10), multiply.s(2)).apply_async()
print(result.get())  # 30
```

In the above example, `chain(add.s(5, 10), multiply.s(2))` creates a chain where the `multiply` task depends on the result of the `add` task. Calling `apply_async()` on the chain schedules all the tasks for execution.

## Conclusion

Handling task results is an important aspect of working with Python Celery. Whether you are using synchronous or asynchronous task execution, knowing how to retrieve and handle task results is crucial. In this article, we explored different ways to handle task results using Celery's `AsyncResult` object, callbacks, and task chains.