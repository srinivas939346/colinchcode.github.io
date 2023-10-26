---
layout: post
title: "[python] Creating RESTful APIs with Flask-SQLAlchemy"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In this tutorial, we will learn how to create RESTful APIs using Flask-SQLAlchemy. Flask-SQLAlchemy is an extension for Flask that makes it easy to work with databases. We will be using SQLite as our database for this tutorial.

## Table of Contents
- [Setting Up Flask and Flask-SQLAlchemy](#setting-up-flask-and-flask-sqlalchemy)
- [Defining Models](#defining-models)
- [Creating API Endpoints](#creating-api-endpoints)
- [Testing the API](#testing-the-api)

## Setting Up Flask and Flask-SQLAlchemy
To get started, we need to install Flask and Flask-SQLAlchemy. If you haven't already, you can install them by running the following commands:

```python
pip install flask
pip install flask_sqlalchemy
```

Once Flask and Flask-SQLAlchemy are installed, we can create a new Flask application and configure the database connection. Here's an example:

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///database.db'  # SQLite database file path
db = SQLAlchemy(app)

if __name__ == '__main__':
    app.run()
```

## Defining Models
The next step is to define our models, which will represent the database tables. We will define a `User` model with a `name` and `email` field. Here's an example:

```python
from datetime import datetime

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(50), nullable=False)
    email = db.Column(db.String(50), unique=True, nullable=False)
    created_at = db.Column(db.DateTime, default=datetime.utcnow)

    def __repr__(self):
        return f'<User {self.name}>'
```

## Creating API Endpoints
Now, let's create the API endpoints for our `User` model. We will create endpoints for listing all users, creating a new user, updating a user, and deleting a user. Here's an example:

```python
from flask import jsonify, request

@app.route('/users', methods=['GET'])
def get_users():
    users = User.query.all()
    return jsonify([{'id': u.id, 'name': u.name, 'email': u.email} for u in users])

@app.route('/users', methods=['POST'])
def create_user():
    data = request.get_json()
    user = User(name=data['name'], email=data['email'])
    db.session.add(user)
    db.session.commit()
    return jsonify({'message': 'User created successfully'})

@app.route('/users/<int:user_id>', methods=['PUT'])
def update_user(user_id):
    user = User.query.get_or_404(user_id)
    data = request.get_json()
    user.name = data['name']
    user.email = data['email']
    db.session.commit()
    return jsonify({'message': 'User updated successfully'})

@app.route('/users/<int:user_id>', methods=['DELETE'])
def delete_user(user_id):
    user = User.query.get_or_404(user_id)
    db.session.delete(user)
    db.session.commit()
    return jsonify({'message': 'User deleted successfully'})
```

## Testing the API
To test the API endpoints, you can use tools like Postman or cURL. Here are some example requests:

- **GET /users**: Retrieve all users.
- **POST /users**: Create a new user. Provide the user's name and email in the request body.
- **PUT /users/{user_id}**: Update a user. Provide the user's name and email in the request body.
- **DELETE /users/{user_id}**: Delete a user.

That's it! You have successfully created RESTful APIs using Flask-SQLAlchemy. You can now build more complex APIs by adding models and endpoints as needed.

References:
- [Flask documentation](https://flask.palletsprojects.com/)
- [Flask-SQLAlchemy documentation](https://flask-sqlalchemy.palletsprojects.com/)