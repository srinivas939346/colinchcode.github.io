---
layout: post
title: "[python] SQLAlchemy Relationships: One-to-One"
description: " "
date: 2023-10-04
tags: [python]
comments: true
share: true
---

When working with databases using SQLAlchemy, it's common to encounter scenarios where a one-to-one relationship needs to be established between two entities. In this blog post, we will explore how to define and utilize such relationships using SQLAlchemy.

## Table Setup

Let's consider a simple scenario where we have two tables: `User` and `Profile`. Each user can have one profile associated with them. The `User` table has columns for `id`, `username`, and `email`, while the `Profile` table has columns for `id`, `bio`, and `user_id` (which serves as the foreign key to establish the relationship).

Here's how we can define these tables using SQLAlchemy:

```python
from sqlalchemy import Column, Integer, String, ForeignKey
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

class User(Base):
    __tablename__ = 'users'
    
    id = Column(Integer, primary_key=True)
    username = Column(String(50), unique=True, nullable=False)
    email = Column(String(100), unique=True, nullable=False)
    
class Profile(Base):
    __tablename__ = 'profiles'
    
    id = Column(Integer, primary_key=True)
    bio = Column(String(250))
    user_id = Column(Integer, ForeignKey('users.id'), unique=True)
```

## Establishing the One-to-One Relationship

To establish the one-to-one relationship between the `User` and `Profile` tables, we will need to define a relationship attribute in the `User` class and use the `uselist` parameter to specify that only one profile can be associated with each user.

```python
from sqlalchemy.orm import relationship

class User(Base):
    __tablename__ = 'users'
    
    id = Column(Integer, primary_key=True)
    username = Column(String(50), unique=True, nullable=False)
    email = Column(String(100), unique=True, nullable=False)
    
    profile = relationship("Profile", back_populates="user", uselist=False)

class Profile(Base):
    __tablename__ = 'profiles'
    
    id = Column(Integer, primary_key=True)
    bio = Column(String(250))
    user_id = Column(Integer, ForeignKey('users.id'), unique=True)
    
    user = relationship("User", back_populates="profile")
```

By setting `uselist=False`, we specify that the relationship should not be represented as a list and only hold a single `Profile` instance.

## Interacting with the One-to-One Relationship

Once the relationship is established, we can easily access the associated profile for a user or vice versa. Here are a couple of examples on how to interact with the one-to-one relationship:

```python
# Creating a new user with a profile
user = User(username="john_doe", email="john@example.com")
profile = Profile(bio="I am John Doe's profile")
user.profile = profile

# Accessing the profile of a user
user = session.query(User).filter_by(username="john_doe").first()
profile = user.profile
print(profile.bio)

# Accessing the user of a profile
profile = session.query(Profile).filter_by(bio="I am John Doe's profile").first()
user = profile.user
print(user.username)
```

## Conclusion

In this blog post, we learned how to establish a one-to-one relationship between two tables using SQLAlchemy. By defining the relationship attribute and specifying `uselist=False`, we can easily work with associated entities. SQLAlchemy provides a powerful and flexible ORM framework that simplifies database relationships and allows for efficient data manipulation.