---
layout: post
title: "[python] Integrating Tortoise ORM with web frameworks (e.g., Flask, Django)"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When developing web applications, it is common to use an Object-Relational Mapping (ORM) tool to interact with the database. Tortoise ORM is a powerful and easy-to-use ORM for Python, which supports asynchronous programming and works great with popular web frameworks like Flask and Django.

In this blog post, we will explore how to integrate Tortoise ORM with web frameworks to build a scalable and efficient web application.

## Table of Contents
- [What is Tortoise ORM?](#what-is-tortoise-orm)
- [Integrating Tortoise ORM with Flask](#integrating-tortoise-orm-with-flask)
- [Integrating Tortoise ORM with Django](#integrating-tortoise-orm-with-django)
- [Conclusion](#conclusion)

## What is Tortoise ORM?
Tortoise ORM is an asyncio ORM for Python and is compatible with both synchronous and asynchronous programming. It provides a simple and intuitive way to interact with databases using Python code, abstracting away the complexities of database queries and enabling developers to focus more on the application logic.

## Integrating Tortoise ORM with Flask
Flask is a minimalist web framework for Python that is widely used for building small to medium-sized web applications. To integrate Tortoise ORM with Flask, follow these steps:

1. Install the required dependencies by running the following command:
    ```
    pip install tortoise-orm[asyncpg]
    ```

2. Create a Tortoise ORM connection configuration. This includes specifying the database connection URL, database name, username, password, etc. For example:
    ```python
    DATABASES = {
        "default": {
            "engine": "tortoise.backends.asyncpg",
            "credentials": {
                "database": "mydatabase",
                "host": "localhost",
                "port": "5432",
                "user": "myuser",
                "password": "mypassword",
            },
        }
    }
    ```

3. Initialize Tortoise ORM by importing and initializing it in your Flask application. For example:
    ```python
    from tortoise import Tortoise, run_async

    app = Flask(__name__)

    @app.before_first_request
    async def init_orm():
        await Tortoise.init(config=DATABASES)
        await Tortoise.generate_schemas()

    @app.route("/")
    async def index():
        # Your code goes here

    if __name__ == "__main__":
        run_async(init_orm())
        app.run()
    ```

4. You can now start using Tortoise ORM in your Flask routes or views to query the database. For example:
    ```python
    from tortoise.contrib.fastapi import register_tortoise

    @app.route("/users")
    async def get_users():
        users = await models.User.all()
        return jsonify([user.to_dict() for user in users])
    ```

## Integrating Tortoise ORM with Django
Django is a popular web framework for Python that follows the Model-View-Controller (MVC) architectural pattern. To integrate Tortoise ORM with Django, follow these steps:

1. Install the required dependencies by running the following command:
    ```
    pip install tortoise-orm[asyncpg]
    ```

2. Update your Django settings file (`settings.py`) to include the Tortoise ORM configuration. For example:
    ```python
    DATABASES = {
        'default': {
            'ENGINE': 'tortoise.backends.asyncpg',
            'NAME': 'mydatabase',
            'HOST': 'localhost',
            'PORT': '5432',
            'USER': 'myuser',
            'PASSWORD': 'mypassword',
        }
    }
    ```

3. In your Django project's `urls.py`, add the following code to initialize Tortoise ORM:
    ```python
    from tortoise import Tortoise, run_async

    async def init_orm():
        await Tortoise.init(config=DATABASES)
        await Tortoise.generate_schemas()

    run_async(init_orm())
    ```

4. You can now define your Tortoise ORM models in the `models.py` file within your Django app. For example:
    ```python
    from tortoise import fields, models

    class User(models.Model):
        id = fields.IntField(pk=True)
        name = fields.CharField(max_length=255)

        def __str__(self):
            return self.name
    ```

5. You can use Tortoise ORM models within your Django views or APIs to perform database operations. For example:
    ```python
    from django.http import JsonResponse
    from myapp.models import User

    def get_users(request):
        users = User.all().values()
        return JsonResponse(list(users), safe=False)
    ```

## Conclusion
Integrating Tortoise ORM with web frameworks like Flask and Django allows developers to leverage the power and flexibility of Tortoise ORM in building web applications. By following the steps mentioned in this blog post, you can easily incorporate Tortoise ORM into your existing or new Python web applications, making the database interaction seamless and efficient. Tortoise ORM's support for asynchronous programming further enhances the scalability and performance of your web applications. Give it a try and experience the simplicity and power of Tortoise ORM in your next web project!