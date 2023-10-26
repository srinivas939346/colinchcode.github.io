---
layout: post
title: "[python] Pagination of query results in Flask-SQLAlchemy"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In web applications, it's common to retrieve a large number of database records for display. However, displaying all the records at once can have a negative impact on performance and user experience. To address this issue, it's recommended to implement pagination, which allows fetching and displaying a limited number of records per page.

Flask-SQLAlchemy, an extension for Flask, makes it easy to handle database operations in Flask applications. In this blog post, we'll explore how to implement pagination of query results using Flask-SQLAlchemy.

## 1. Setting up Flask-SQLAlchemy

First, make sure you have Flask-SQLAlchemy installed. You can install it using pip:

```python
pip install flask-sqlalchemy
```

Next, initialize Flask-SQLAlchemy in your Flask application:

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///database.db'
db = SQLAlchemy(app)
```

In the above code, we import the necessary modules, create a Flask application, and set the database URI. Modify the URI based on your database configuration.

## 2. Creating a Model

Let's assume we have a `User` model representing user records in the database. Here's an example implementation:

```python
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(100))
    email = db.Column(db.String(100))

    def __init__(self, name, email):
        self.name = name
        self.email = email
```

Make sure you have defined the necessary columns for your model. This example assumes that the primary key is an integer, and the `name` and `email` fields are strings.

## 3. Fetching Paginated Records

To fetch paginated records, you can use the `paginate` method provided by Flask-SQLAlchemy. Here's an example:

```python
from flask import request

@app.route('/users')
def get_users():
    page = request.args.get('page', default=1, type=int)
    per_page = request.args.get('per_page', default=10, type=int)

    users = User.query.paginate(page=page, per_page=per_page)
    return render_template('users.html', users=users)
```

In the above code, we define a route `/users` that fetches the paginated user records. The `paginate` method takes two parameters - `page` and `per_page`. We retrieve these values from the request arguments.

The `paginate` method returns a `Pagination` object, which contains the paginated records. We pass this object to the template for rendering.

## 4. Displaying Pagination Links

To display links for navigating between pages, Flask-SQLAlchemy provides the `prev()` and `next()` methods on the `Pagination` object. Here's an example of how to display pagination links in a template:

```html
{% for page in users.iter_pages() %}
    {% if page %}
        {% if users.page == page %}
            <span>{{ page }}</span>
        {% else %}
            <a href="{{ url_for('get_users', page=page) }}">{{ page }}</a>
        {% endif %}
    {% else %}
        <span class="ellipsis">...</span>
    {% endif %}
{% endfor %}
```

In the above code, we iterate over the pages using the `iter_pages()` method. We check if the current iteration is the current page and render it as plain text. Otherwise, we render a link to the respective page using the `url_for` function.

## Conclusion

Implementing pagination of query results is crucial for optimizing performance and improving user experience in web applications. Flask-SQLAlchemy provides a convenient way to paginate query results in Flask applications.

In this blog post, we covered how to set up Flask-SQLAlchemy, create a model, fetch paginated records, and display pagination links. By following these steps, you can easily implement pagination of query results in your Flask-SQLAlchemy applications.

If you have any questions or suggestions, feel free to leave a comment below.

References:
- [Flask-SQLAlchemy Documentation](https://flask-sqlalchemy.palletsprojects.com/)
- [Flask Documentation](https://flask.palletsprojects.com/)