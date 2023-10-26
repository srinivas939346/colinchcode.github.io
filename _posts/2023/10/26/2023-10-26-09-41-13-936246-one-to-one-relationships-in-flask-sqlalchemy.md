---
layout: post
title: "[python] One-to-one relationships in Flask-SQLAlchemy"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

One key aspect of relational databases is the ability to establish relationships between tables. In Flask-SQLAlchemy, you can define various types of relationships, including one-to-one relationships.

A one-to-one relationship occurs when one entity in a table is associated with exactly one entity in another table. For example, consider a scenario where we have two tables: `User` and `Profile`. Each user has one profile, and each profile belongs to one user.

## Defining the models

To establish a one-to-one relationship between the `User` and `Profile` tables, we need to define the models accordingly. Here is an example of how we can do this using Flask-SQLAlchemy:

```python
from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(50), nullable=False)
    profile = db.relationship('Profile', backref='user', uselist=False)

class Profile(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    bio = db.Column(db.Text)
    user_id = db.Column(db.Integer, db.ForeignKey('user.id'), unique=True)
```

In the `User` model, we define a `profile` attribute using the `db.relationship` function. This establishes the one-to-one relationship with the `Profile` model. The `backref` argument creates a virtual column `user` in the `Profile` model, which can be used to access the associated user.

The `Profile` model has a `user_id` column, which is a foreign key referencing the `id` column of the `User` model. This establishes the link between the two tables.

## Creating and accessing the relationship

Once the models are defined, we can create and access the one-to-one relationship. Here is an example:

```python
# Create a user and profile
user = User(name='John Doe')
profile = Profile(bio='A software developer')
user.profile = profile

# Save the user and profile to the database
db.session.add(user)
db.session.commit()

# Access the associated profile from a user
print(user.profile.bio)  # Output: A software developer

# Access the associated user from a profile
print(profile.user.name)  # Output: John Doe
```

In the above example, we first create an instance of the `User` model and an instance of the `Profile` model. We then assign the profile to the user using the `profile` attribute.

After adding the user to the database, we can access the associated profile using the `profile` attribute of the user instance. Similarly, we can access the associated user using the `user` attribute of the profile instance.

## Conclusion

Establishing a one-to-one relationship in Flask-SQLAlchemy is straightforward. By defining the appropriate models and using the `db.relationship` function, you can easily create and access one-to-one relationships in your Flask application.

For more information on Flask-SQLAlchemy and its relationship features, refer to the [official documentation](https://flask-sqlalchemy.palletsprojects.com/).