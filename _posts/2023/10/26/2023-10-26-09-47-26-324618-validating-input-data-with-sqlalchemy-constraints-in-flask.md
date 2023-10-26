---
layout: post
title: "[python] Validating input data with SQLAlchemy constraints in Flask"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When building a web application, it is essential to validate the input data before it is stored in the database. One way to achieve this in Flask is by using SQLAlchemy constraints. SQLAlchemy is a popular Object Relational Mapper (ORM) library that provides a powerful and flexible way to interact with databases.

## Installing SQLAlchemy

First, make sure you have SQLAlchemy installed. You can install it using pip:

```
pip install SQLAlchemy
```

## Creating a Flask application

Let's start by creating a basic Flask application that will handle user registration. Create a new file called `app.py` and add the following code:

```python
from flask import Flask, render_template, request
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///users.db'
db = SQLAlchemy(app)

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(100), nullable=False)
    email = db.Column(db.String(100), nullable=False, unique=True)
    age = db.Column(db.Integer, nullable=False)

    def __repr__(self):
        return f"<User {self.name}>"

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/register', methods=['POST'])
def register():
    name = request.form.get('name')
    email = request.form.get('email')
    age = request.form.get('age')

    new_user = User(name=name, email=email, age=age)
    db.session.add(new_user)
    db.session.commit()

    return "User registered successfully!"

if __name__ == '__main__':
    app.run(debug=True)
```

In the above code, we define a `User` model with three attributes: `name`, `email`, and `age`. The `name` and `email` attributes have a `nullable=False` constraint, which means they cannot be empty. Additionally, the `email` attribute has a `unique=True` constraint, which ensures that each email address is unique.

The `register` function handles the user registration process. It retrieves the form data from the request and creates a new `User` object. If the data passes the validation constraints, it is stored in the database using SQLAlchemy's `session` object.

## Creating HTML templates

To complete our application, we need to create the HTML templates. Create a new folder called `templates` and inside it, create a file called `index.html` with the following content:

```html
<!DOCTYPE html>
<html>
<head>
    <title>User Registration</title>
</head>
<body>
    <h1>User Registration</h1>
    <form action="/register" method="post">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required>
        <br>
        <label for="email">Email:</label>
        <input type="email" id="email" name="email" required>
        <br>
        <label for="age">Age:</label>
        <input type="number" id="age" name="age" required>
        <br>
        <input type="submit" value="Register">
    </form>
</body>
</html>
```

This template defines a simple form where users can enter their name, email, and age. The form's `action` attribute is set to `/register`, which corresponds to the `register` route in our Flask application.

## Testing the application

To test the application, run the following command in your terminal:

```
python app.py
```

You should see output similar to the following:

```
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

Open your web browser and navigate to `http://127.0.0.1:5000/`. You should see the user registration form. Enter some data and click on the "Register" button. If the data passes the validation constraints, you should see the "User registered successfully!" message.

## Conclusion

In this blog post, we have explored how to use SQLAlchemy constraints in a Flask application to validate input data before storing it in the database. By defining constraints on the model's attributes, we ensure that the data meets our requirements. This approach enhances data integrity and reduces the risk of storing erroneous data in the database.

References:
- [SQLAlchemy Documentation](https://docs.sqlalchemy.org/)
- [Flask Documentation](https://flask.palletsprojects.com/)