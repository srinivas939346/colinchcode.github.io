---
layout: post
title: "[python] SQLAlchemy Relationships: Many-to-Many"
description: " "
date: 2023-10-04
tags: [python]
comments: true
share: true
---

In this blog post, we will dive into one of the most powerful features of the SQLAlchemy ORM - the ability to handle many-to-many relationships between database tables. Many-to-many relationships occur when multiple rows in one table are related to multiple rows in another table.

## Table Setup

Let's start by creating two tables, `users` and `roles`, that we will use to demonstrate the many-to-many relationship.

```python
from sqlalchemy import create_engine, Column, Integer, String, Table
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import relationship

Base = declarative_base()

users_roles = Table(
    "users_roles",
    Base.metadata,
    Column("user_id", Integer, ForeignKey("users.id")),
    Column("role_id", Integer, ForeignKey("roles.id"))
)

class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    name = Column(String)
    roles = relationship("Role", secondary=users_roles, backref="users")

class Role(Base):
    __tablename__ = 'roles'
    id = Column(Integer, primary_key=True)
    name = Column(String)
```

In the above code, we define two tables, `users` and `roles`, and a many-to-many relationship between them using the `users_roles` association table.

## Creating and Querying Data

Now that we have our table setup, let's create some data and query it.

```python
engine = create_engine("sqlite:///test.db")
Base.metadata.create_all(engine)

session = Session(engine)

# Create users
user1 = User(name="John")
user2 = User(name="Jane")
user3 = User(name="Alice")

# Create roles
role1 = Role(name="Admin")
role2 = Role(name="Editor")
role3 = Role(name="Viewer")

# Assign roles to users
user1.roles.append(role1)
user1.roles.append(role2)
user2.roles.append(role2)
user3.roles.append(role3)

# Commit changes to the database
session.add_all([user1, user2, user3])
session.commit()

# Query users with their roles
users = session.query(User).all()

for user in users:
    print(f"User: {user.name}")
    for role in user.roles:
        print(f"Role: {role.name}")
```

In the code above, we create several users and roles and assign roles to users using the `roles` attribute. Finally, we query the users along with their roles and print the results.

## Conclusion

SQLAlchemy provides a convenient way to handle many-to-many relationships in your database models. By defining an association table and using the `relationship` and `secondary` parameters, you can easily manage and query data across multiple tables.

In this blog post, we covered the basics of creating and querying many-to-many relationships using SQLAlchemy. Feel free to explore more advanced features and techniques to take full advantage of the powerful ORM.