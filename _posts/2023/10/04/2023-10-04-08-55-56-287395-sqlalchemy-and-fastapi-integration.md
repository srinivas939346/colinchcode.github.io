---
layout: post
title: "[python] SQLAlchemy and FastAPI Integration"
description: " "
date: 2023-10-04
tags: [python]
comments: true
share: true
---

In this tutorial, we will explore how to integrate SQLAlchemy, a powerful Object-Relational Mapping (ORM) library, with FastAPI, a modern, fast (high-performance) web framework for building APIs with Python.

## Table of Contents

1. [Introduction to SQLAlchemy](#introduction-to-sqlalchemy)
2. [Setting up the Database](#setting-up-the-database)
3. [Creating the SQLAlchemy Models](#creating-the-sqlalchemy-models)
4. [Connecting SQLAlchemy with FastAPI](#connecting-sqlalchemy-with-fastapi)
5. [Using SQLAlchemy in FastAPI Routes](#using-sqlalchemy-in-fastapi-routes)

## Introduction to SQLAlchemy

SQLAlchemy is a SQL toolkit and Object-Relational Mapping (ORM) library for Python. It provides a set of high-level API for interacting with databases, making it easier to work with relational databases in your Python applications. SQLAlchemy supports multiple database management systems including SQLite, MySQL, PostgreSQL, and more.

## Setting up the Database

Before we can start integrating SQLAlchemy with FastAPI, we need to set up a database. For this tutorial, we will be using SQLite as our database.

You can install SQLite by running the following command:

```bash
$ pip install sqlite-python
```

After installing SQLite, create a new file called `database.db` that will serve as our SQLite database.

## Creating the SQLAlchemy Models

The next step is to define our SQLAlchemy models. Models in SQLAlchemy are Python classes that represent database tables. Each attribute of the model class corresponds to a column in the table.

```python
# models.py

from sqlalchemy import Boolean, Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True, index=True)
    name = Column(String, index=True)
    email = Column(String, unique=True, index=True)
    password = Column(String)
    is_active = Column(Boolean, default=True)
```

In the code above, we define a `User` model with four columns: `id`, `name`, `email`, and `password`. We also include a `is_active` column, which defaults to `True`.

## Connecting SQLAlchemy with FastAPI

To connect SQLAlchemy with FastAPI, we need to establish a database connection and create a SQLAlchemy `Session` object. We will use a dependency injection technique provided by FastAPI to achieve this.

```python
# main.py

from fastapi import Depends, FastAPI
from sqlalchemy import create_engine
from sqlalchemy.orm import Session, sessionmaker

from models import Base, User

app = FastAPI()

SQLALCHEMY_DATABASE_URL = "sqlite:///./database.db"

engine = create_engine(SQLALCHEMY_DATABASE_URL)
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

Base.metadata.create_all(bind=engine)
```

In the code above, we create a SQLAlchemy engine using the SQLite database URL and define a `SessionLocal` object that will serve as our database session. The `get_db()` function is a dependency that will provide a SQLAlchemy session to our route functions.

## Using SQLAlchemy in FastAPI Routes

Now that we have set up the integration between SQLAlchemy and FastAPI, we can start using SQLAlchemy in our route functions.

```python
# main.py (continued)

@app.post("/users/")
def create_user(user: UserCreate, db: Session = Depends(get_db)):
    new_user = User(name=user.name, email=user.email, password=user.password)
    db.add(new_user)
    db.commit()
    db.refresh(new_user)
    return new_user

@app.get("/users/{user_id}")
def get_user(user_id: int, db: Session = Depends(get_db)):
    user = db.query(User).filter(User.id == user_id).first()
    if not user:
        raise HTTPException(status_code=404, detail="User not found")
    return user
```

In the code above, we define two route functions: `create_user()` and `get_user()`. The `create_user()` function receives a `UserCreate` object as input, creates a new user in the database, and returns the created user. The `get_user()` function retrieves a user from the database based on the provided `user_id`.

That's it! We have successfully integrated SQLAlchemy with FastAPI. Now you can use the power of SQLAlchemy to build robust and efficient APIs with FastAPI.

Remember to install the required dependencies:

```bash
$ pip install fastapi sqlalchemy
```

Happy coding!