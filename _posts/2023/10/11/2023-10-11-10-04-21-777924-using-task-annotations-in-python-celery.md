---
layout: post
title: "[python] Using task annotations in Python Celery"
description: " "
date: 2023-10-11
tags: [python]
comments: true
share: true
---

Celery is a distributed task queue library in Python that allows you to run tasks asynchronously. With Celery, you can divide your application into smaller tasks and distribute them across multiple worker nodes for parallel execution.

One of the features introduced in Celery 5.0 is task annotations, which provide a more concise and declarative way to define task metadata such as the task name, task time limit, and task retry behavior. In this blog post, we will explore how to use task annotations in Python Celery.

## What are Task Annotations?

Traditionally, you define a Celery task by creating a function and decorating it with the `@task` decorator. The task metadata, such as the task name or task time limit, is specified using additional decorator arguments or by setting attributes on the task function object.

Task annotations provide an alternative way to define task metadata by using Python function annotations. Instead of applying decorators, you can simply annotate your task functions with special annotations that Celery recognizes.

## Annotating Task Metadata

To use task annotations, you need to define your task functions with annotations that specify the desired metadata. Here's an example:

```python
from celery import Celery

app = Celery('myapp', broker='redis://localhost:6379/0')

@app.task
def add(x: int, y: int) -> int:
    return x + y

@app.task(bind=True, name='myapp.tasks.multiply', time_limit=30)
def multiply(self, x: int, y: int) -> int:
    return x * y
```

In the above example, we have defined two tasks: `add` and `multiply`. The `add` task takes two integers as input and returns their sum. The `multiply` task also takes two integers as input, but it has additional metadata specified using task annotations.

The `multiply` task is annotated with `bind=True`, which binds the task instance to the first argument (typically named `self`). This allows you to access task-specific attributes and methods within the task function.

We have also specified the task name as `'myapp.tasks.multiply'` using the `name` annotation. This overrides the default task name derived from the function name.

The `time_limit` annotation sets a time limit of 30 seconds for executing the task. If the task execution exceeds this time limit, it will be terminated.

## Benefits of Task Annotations

Using task annotations has several benefits:

1. **Cleaner and more readable code**: Task annotations provide a more concise and declarative way to define task metadata. You can see the task metadata right alongside the function signature, making it easier to understand and maintain.

2. **Separation of concerns**: Task annotations separate the task-specific metadata from the task logic. This makes it easier to modify or extend the task metadata without touching the task implementation.

3. **Better tooling support**: Task annotations make it easier for IDEs and code analysis tools to provide intelligent suggestions and validations when working with Celery tasks. IDEs can recognize the annotations and provide autocompletion, type checking, and documentation assistance.

## Conclusion

Task annotations in Python Celery provide a more concise and declarative way to define task metadata. By using function annotations, you can specify task name, time limit, and other metadata right alongside the task function. Task annotations make your code cleaner, easier to understand, and maintainable. They also improve tooling support and provide benefits like separation of concerns. So, the next time you work with Celery, consider using task annotations to enhance your task definitions.