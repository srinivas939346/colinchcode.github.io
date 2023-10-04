---
layout: post
title: "[python] SQLAlchemy and Starlette Integration"
description: " "
date: 2023-10-04
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to integrate SQLAlchemy and Starlette, two powerful libraries in the Python ecosystem, to build a robust and scalable web application.

## Table of Contents
- [Introduction](#introduction)
- [Setting up the Database](#setting-up-the-database)
- [Defining the Model](#defining-the-model)
- [Creating a Session](#creating-a-session)
- [Querying the Database](#querying-the-database)
- [Adding CRUD Operations](#adding-crud-operations)
- [Conclusion](#conclusion)

## Introduction

Starlette is a lightweight, high-performance web framework for building APIs and web applications. SQLAlchemy is a SQL toolkit and Object-Relational Mapping (ORM) library that provides a set of high-level API for connecting with databases.

By integrating SQLAlchemy with Starlette, we can leverage SQLAlchemy's rich features for database operations and easily build a RESTful API or web application.

## Setting up the Database

First, we need to install the necessary packages:

```python
pip install sqlalchemy
pip install databases
```

Next, we need to set up a database connection. For this example, let's assume we are using SQLite.

```python
from starlette.config import Config
from sqlalchemy import create_engine

config = Config('.env')
DATABASE_URL = config('DATABASE_URL')

engine = create_engine(DATABASE_URL)
```

## Defining the Model

Now, let's define a simple model using SQLAlchemy's declarative base class. We'll create a `User` model with two attributes: `id` and `name`.

```python
from sqlalchemy import Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

class User(Base):
    __tablename__ = 'users'

    id = Column(Integer, primary_key=True)
    name = Column(String)
```

## Creating a Session

To interact with the database, we need a session object. We can use SQLAlchemy's `scoped_session` to create a session that is thread-local and automatically ends when the request is completed.

```python
from sqlalchemy.orm import sessionmaker, scoped_session

SessionLocal = scoped_session(sessionmaker(bind=engine))
```

## Querying the Database

With the model and session in place, we can now perform database queries using SQLAlchemy's API. Let's query all users from the database.

```python
with SessionLocal() as session:
    users = session.query(User).all()

    for user in users:
        print(f"User ID: {user.id}, Name: {user.name}")
```

## Adding CRUD Operations

To complete the integration, we can add Create, Read, Update, and Delete (CRUD) operations to our API. Here's an example of a simple RESTful API endpoint using Starlette and SQLAlchemy:

```python
from starlette.applications import Starlette
from starlette.requests import Request
from starlette.responses import JSONResponse
from sqlalchemy.exc import IntegrityError

app = Starlette()

@app.route('/users', methods=['GET', 'POST'])
async def users(request: Request):
    if request.method == 'GET':
        with SessionLocal() as session:
            users = session.query(User).all()
            return JSONResponse([{'id': user.id, 'name': user.name} for user in users])

    if request.method == 'POST':
        data = await request.json()
        user = User(name=data['name'])

        with SessionLocal() as session:
            try:
                session.add(user)
                session.commit()
                return JSONResponse({'message': 'User created successfully'})
            except IntegrityError:
                session.rollback()
                return JSONResponse({'error': 'User with the same name already exists'}, status_code=400)
```

## Conclusion

Integrating SQLAlchemy with Starlette allows us to build powerful and scalable web applications with ease. We have seen how to set up the database connection, define a model, perform database queries, and add CRUD operations to our API.

By leveraging the strengths of both libraries, we can build robust and efficient applications that interact seamlessly with the database.