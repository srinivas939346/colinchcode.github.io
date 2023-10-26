---
layout: post
title: "[python] Seeding the database with initial data using Flask-SQLAlchemy"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When developing web applications with Flask and using SQLAlchemy as the ORM (Object-Relational Mapping) tool, it is often necessary to seed the database with initial data. Seeding the database means populating it with predefined data that will be used for testing or as default values.

In this article, we will explore how to seed a database using Flask-SQLAlchemy. We will assume that you have already set up a Flask project with SQLAlchemy installed.

### 1. Create a Seed Data Module

First, let's create a Python module for our seed data. Create a file called `seed_data.py` in your project directory. This module will contain the code to populate the database with the initial data.

```python
# seed_data.py

from app import db
from app.models import User

def seed_users():
    user1 = User(username='john', email='john@example.com')
    user2 = User(username='jane', email='jane@example.com')
    
    db.session.add(user1)
    db.session.add(user2)
    db.session.commit()
```

In this example, we assume that you have a `User` model defined in your `app.models` module. Adjust the import statements as necessary to match your project structure.

### 2. Create a Database Seeder Script

Next, let's create a Python script that will run the seed data function. Create a file called `seed_database.py` in your project directory. This script will import the `seed_users` function from the `seed_data` module and execute it.

```python
# seed_database.py

from app import create_app
from seed_data import seed_users

app = create_app()

with app.app_context():
    seed_users()
```

In this script, we assume that you have a Flask application factory function called `create_app` defined in your `app` module. Adjust the import statements as necessary to match your project structure.

### 3. Run the Seeder Script

To run the seeder script and populate the database with the initial data, simply execute the following command in your terminal:

```shell
python seed_database.py
```

Make sure you are in the root directory of your project when running this command.

### Conclusion

Seeding the database with initial data is a common task when developing Flask applications. By creating a seed data module and a database seeder script, you can easily populate your database with predefined data for testing or as default values.

Remember to adjust the code snippets according to your specific project structure and data requirements.

---

References:
- [Flask-SQLAlchemy Documentation](https://flask-sqlalchemy.palletsprojects.com/)