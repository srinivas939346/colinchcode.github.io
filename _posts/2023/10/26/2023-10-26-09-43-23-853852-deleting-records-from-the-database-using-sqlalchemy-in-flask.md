---
layout: post
title: "[python] Deleting records from the database using SQLAlchemy in Flask"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When working with web applications built using Flask, SQLAlchemy is a popular choice for database management. In this blog post, we'll explore how to delete records from the database using SQLAlchemy within a Flask application.

## Table of Contents
- [Setting up SQLAlchemy](#setting-up-sqlalchemy)
- [Deleting records using SQLAlchemy](#deleting-records-using-sqlalchemy)
- [Example Code](#example-code)
- [Conclusion](#conclusion)
- [References](#references)

## Setting up SQLAlchemy

Before we can start deleting records, we need to set up SQLAlchemy within our Flask application. First, let's install SQLAlchemy using pip:

```python
pip install flask-sqlalchemy
```

Next, let's import the necessary modules in our Flask application's main file:

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy
```

We also need to configure the database connection URL in our application's configuration:

```python
app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///database.db'
db = SQLAlchemy(app)
```

With these steps, we now have SQLAlchemy set up and ready to delete records from the database.

## Deleting records using SQLAlchemy

To delete records from the database using SQLAlchemy, we can make use of the `delete()` method provided by SQLAlchemy's query object. This method allows us to specify the conditions for deletion using filters.

Here's an example of how to delete records from a table called `users`:

```python
from models import User

# Delete a single record
user = User.query.filter_by(id=1).first()
db.session.delete(user)
db.session.commit()

# Delete multiple records based on a condition
User.query.filter(User.age > 30).delete()
db.session.commit()
```

In the first example, we delete a single record by specifying its primary key. We retrieve the record using the `filter_by()` method and `first()` function, then call the `delete()` method on the query object. Finally, we commit the changes to the database using `db.session.commit()`.

In the second example, we delete multiple records based on a condition. We use the `filter()` method to specify the condition and then call the `delete()` method directly on the query object. Again, we need to commit the changes using `db.session.commit()`.

## Example Code

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///database.db'
db = SQLAlchemy(app)

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(50))
    age = db.Column(db.Integer)

# Delete a single record
user = User.query.filter_by(id=1).first()
db.session.delete(user)
db.session.commit()

# Delete multiple records based on a condition
User.query.filter(User.age > 30).delete()
db.session.commit()
```

## Conclusion

In this blog post, we learned how to delete records from the database using SQLAlchemy in a Flask application. We explored the setup process for SQLAlchemy and demonstrated examples of deleting both single and multiple records.

By leveraging the power of SQLAlchemy, working with databases in Flask becomes a breeze, allowing us to efficiently manage our data.

## References
- [Flask SQLAlchemy Documentation](https://flask-sqlalchemy.palletsprojects.com/)
- [SQLAlchemy Documentation](https://docs.sqlalchemy.org/)