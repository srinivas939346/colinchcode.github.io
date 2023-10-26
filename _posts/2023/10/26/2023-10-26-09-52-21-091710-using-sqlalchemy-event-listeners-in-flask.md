---
layout: post
title: "[python] Using SQLAlchemy event listeners in Flask"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

SQLAlchemy is a powerful and flexible Object-Relational Mapping (ORM) library for Python. It allows you to interact with relational databases using high-level Python objects. One of the features that SQLAlchemy provides is event listeners, which allow you to define functions that are executed when certain events occur on your database models.

In this blog post, we will explore how to use SQLAlchemy event listeners in a Flask application. We will use a simple example of a blog application with a `Post` model.

## Prerequisites
Before diving into the code, make sure you have the following installed:
- Python
- Flask
- SQLAlchemy

## Setting Up the Project
Let's start by creating a new Flask project and installing SQLAlchemy. Create a new virtual environment and activate it:

```bash
$ python3 -m venv myenv
$ source myenv/bin/activate
```

Install Flask and SQLAlchemy using pip:

```bash
$ pip install Flask SQLAlchemy
```

Create a new file `app.py` and initialize the Flask application:

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///blog.db'
db = SQLAlchemy(app)

if __name__ == '__main__':
    app.run()
```

## Defining the Model
Next, let's define our `Post` model in `app.py`:

```python
class Post(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    title = db.Column(db.String(80), nullable=False)
    content = db.Column(db.Text, nullable=False)
    created_at = db.Column(db.DateTime, default=datetime.utcnow)

    def __repr__(self):
        return f"<Post {self.title}>"
```

## Creating an Event Listener
Now, let's create an event listener that will automatically set the `created_at` field of a `Post` model whenever a new post is inserted into the database. Add the following code to `app.py`:

```python
@db.event.listens_for(Post, 'before_insert')
def set_created_at(mapper, connection, target):
    target.created_at = datetime.utcnow()
```

In this example, `before_insert` is the event we are listening to. The `set_created_at` function will be called before a new `Post` object is inserted into the database.

## Testing the Event Listener
To test the event listener, let's create a route in `app.py` that inserts a new post into the database:

```python
@app.route('/add_post')
def add_post():
    post = Post(title='New Post', content='This is a new post')
    db.session.add(post)
    db.session.commit()
    
    return 'Post added successfully!'
```

Now, if you run your Flask application and visit the `/add_post` route, a new post will be inserted into the database with its `created_at` field automatically set.

## Conclusion
In this blog post, we have seen how to use SQLAlchemy event listeners in a Flask application. Event listeners can be powerful tools for adding additional functionality to your database models. They allow you to perform actions automatically when specific events occur.

By incorporating event listeners into your Flask application, you can easily extend the capabilities of your database models and automate certain tasks.

___
References:
- [SQLAlchemy](https://www.sqlalchemy.org/)
- [Flask](https://flask.palletsprojects.com/)
- [Flask-SQLAlchemy](https://flask-sqlalchemy.palletsprojects.com/)