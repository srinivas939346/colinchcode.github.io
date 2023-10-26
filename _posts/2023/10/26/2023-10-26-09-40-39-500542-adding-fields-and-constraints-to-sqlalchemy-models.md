---
layout: post
title: "[python] Adding fields and constraints to SQLAlchemy models"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When working with databases in Python, SQLAlchemy is a commonly used Object-Relational Mapping (ORM) library. It simplifies the process of interacting with databases by allowing you to work with database tables as Python classes.

In this article, we will focus on adding fields and constraints to SQLAlchemy models, which define the structure of the database tables.

### Defining models in SQLAlchemy

Before we dive into adding fields and constraints, let's quickly understand how to define models in SQLAlchemy. Models are defined as Python classes that inherit from SQLAlchemy's `Base` class. Each attribute of the class represents a column in the corresponding database table.

Here's a simple example of defining a `User` model:

```python
from sqlalchemy import Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

class User(Base):
    __tablename__ = 'users'

    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    email = Column(String(100), unique=True)
```

In this example, we define a `User` class that represents a table named "users" in the database. It has columns for `id`, `name`, and `email`, each mapped to the respective class attribute.

### Adding fields to models

To add a new field to a model, simply add a new attribute to the class definition. The attribute should be an instance of the appropriate SQLAlchemy `Column` type. For example, to add a `phone` field to the `User` model, we can modify the class as follows:

```python
class User(Base):
    __tablename__ = 'users'

    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    email = Column(String(100), unique=True)
    phone = Column(String(15))
```

In this case, we added a `phone` column of type `String` with a maximum length of 15 characters.

### Adding constraints to fields

Constraints are rules that define the properties and relationships between fields in a database table. SQLAlchemy provides various constraint types that can be added to fields.

For example, you can add a `NOT NULL` constraint to a field by setting the `nullable` argument of the `Column` to `False`. This ensures that the field must have a value when inserting a new record:

```python
class User(Base):
    __tablename__ = 'users'

    id = Column(Integer, primary_key=True)
    name = Column(String(50), nullable=False)  # NOT NULL constraint
    email = Column(String(100), unique=True)
    phone = Column(String(15))
```

In this case, the `name` field is required and can't be empty.

You can also add other constraints such as `UNIQUE`, `PRIMARY KEY`, `FOREIGN KEY`, and more. SQLAlchemy provides dedicated argument attributes for each constraint type to easily add them to fields.

### Conclusion

In this article, we have explored how to add fields and constraints to SQLAlchemy models. We saw how to define models using Python classes and add new fields by simply adding attributes. We also learned how to add constraints to fields to enforce database rules.

By leveraging these features of SQLAlchemy, you can easily create models that accurately represent your database structure and effectively handle data manipulation tasks. For more details and advanced features, refer to the SQLAlchemy documentation.

**References:**

- [SQLAlchemy Documentation](https://docs.sqlalchemy.org/)
- [SQLAlchemy Core Tutorial](https://docs.sqlalchemy.org/en/14/core/tutorial.html)