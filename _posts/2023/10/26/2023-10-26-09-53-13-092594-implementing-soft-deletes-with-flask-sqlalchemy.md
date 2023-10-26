---
layout: post
title: "[python] Implementing soft deletes with Flask-SQLAlchemy"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In this blog post, we will discuss how to implement soft deletes in a Flask application using Flask-SQLAlchemy. Soft deletes refer to the concept of flagging records as deleted instead of physically deleting them from the database. This approach allows for easy recovery of deleted records and provides a way to preserve data integrity.

### What is Flask-SQLAlchemy?

Flask-SQLAlchemy is an extension for Flask that adds support for SQLAlchemy, a SQL toolkit and Object-Relational Mapping (ORM) library. It provides an easy-to-use interface for interacting with databases in Flask applications.

### Setting up the environment

Before we get started, let's make sure you have Flask-SQLAlchemy installed in your environment. You can install it using pip:

```
$ pip install flask-sqlalchemy
```

### Creating a model

First, let's create a model for our database table. We will be using a simple `User` model for this example:

```python
from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(50))
    is_deleted = db.Column(db.Boolean, default=False, nullable=False)
```

In the `User` model, we have added an additional column called `is_deleted`, which will be used to determine whether a record has been deleted or not.

### Implementing soft deletes

To implement soft deletes in our application, we need to override the default delete behavior of SQLAlchemy's `Query` class. We can achieve this by subclassing `Query` and overriding the `delete` method. Here's an example implementation:

```python
class SoftDeleteQuery(db.Query):

    def delete(self):
        for obj in self.all():
            obj.is_deleted = True
            db.session.add(obj)
        db.session.commit()
```

In the overridden `delete` method, we iterate over all the objects returned by the query and set their `is_deleted` attribute to `True`. We then add them to the session and commit the changes.

### Updating the model query

To use our custom `SoftDeleteQuery` class for querying our models, we need to update the `query_class` attribute in the `User` model. Here's how we can do it:

```python
class User(db.Model):
    # ...
    query_class = SoftDeleteQuery
```

Now, whenever we perform a delete operation on the `User` model, the soft delete behavior will be triggered.

### Filtering deleted records

To filter out deleted records when querying the `User` model, we can create a helper method that modifies the default query behavior:

```python
class User(db.Model):
    # ...

    @classmethod
    def query(cls):
        return super().query.filter(cls.is_deleted == False)
```

In the above example, we override the `query` method and add a filter condition to exclude deleted records from the query results.

### Conclusion

In this blog post, we learned how to implement soft deletes in a Flask application using Flask-SQLAlchemy. By following the steps provided, you can easily flag records as deleted instead of physically deleting them from the database. This approach can help preserve data integrity and allow for easy recovery of deleted records.