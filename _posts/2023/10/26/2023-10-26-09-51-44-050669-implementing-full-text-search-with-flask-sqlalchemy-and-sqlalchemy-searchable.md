---
layout: post
title: "[python] Implementing full-text search with Flask-SQLAlchemy and SQLAlchemy-Searchable"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to implement full-text search functionality in a Flask application using Flask-SQLAlchemy and SQLAlchemy-Searchable. Full-text search allows users to search for specific words or phrases within a text-based database column efficiently.

## Table of Contents
* [Introduction](#introduction)
* [Setting up the Environment](#setting-up-the-environment)
* [Creating the Database Model](#creating-the-database-model)
* [Configuring SQLAlchemy-Searchable](#configuring-sqlalchemy-searchable)
* [Performing Full-text Search](#performing-full-text-search)
* [Conclusion](#conclusion)

## Introduction
Implementing full-text search in a Flask application can be achieved by combining Flask-SQLAlchemy, a lightweight Object Relational Mapping (ORM) library, with SQLAlchemy-Searchable, an extension that provides full-text search capabilities for SQLAlchemy.

## Setting up the Environment
Before we begin, make sure you have Flask, Flask-SQLAlchemy, and SQLAlchemy-Searchable installed in your environment. You can install them by running the following commands:

```bash
pip install Flask
pip install Flask-SQLAlchemy
pip install SQLAlchemy-Searchable
```

## Creating the Database Model
To perform full-text search, we need to define a model that represents the table in our database. Let's create a simple `Article` model with a `title` and `content` column:

```python
from flask_sqlalchemy import SQLAlchemy
from sqlalchemy_searchable import make_searchable

db = SQLAlchemy()

class Article(db.Model):
    __tablename__ = 'articles'

    id = db.Column(db.Integer, primary_key=True)
    title = db.Column(db.String(100))
    content = db.Column(db.Text)

    __searchable_columns__ = ['title', 'content']

make_searchable(db.metadata)
```

In the code above, we define the `Article` model with the `title` and `content` columns. We also set the `__searchable_columns__` attribute to specify which columns should be indexed for full-text search. The `make_searchable` function is called to make the model searchable.

## Configuring SQLAlchemy-Searchable
Next, we need to configure SQLAlchemy-Searchable in our Flask application. Let's create a `create_app` function that initializes the Flask application and configures SQLAlchemy:

```python
from flask import Flask

def create_app():
    app = Flask(__name__)
    app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///articles.db'
    app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
    
    db.init_app(app)
    
    return app
```

In the code above, we create a Flask application, set the SQLite database URI, and disable modification tracking. We then initialize the SQLAlchemy instance with the Flask application.

## Performing Full-text Search
To perform a full-text search, we can use the `query` method provided by SQLAlchemy-Searchable. Let's create a route that accepts a search query parameter and returns the matching articles:

```python
from flask import request

@app.route('/search')
def search():
    query = request.args.get('query')
    articles = Article.query.search(query).all()
    return render_template('search_results.html', articles=articles)
```

In the code above, we retrieve the search query from the `query` parameter in the request. We then use the `search` method provided by SQLAlchemy-Searchable to perform the full-text search and fetch the matching articles. Finally, we pass the articles to the template for display.

## Conclusion
Implementing full-text search in a Flask application using Flask-SQLAlchemy and SQLAlchemy-Searchable is straightforward and efficient. By following the steps outlined in this blog post, you can enable powerful searching capabilities in your application, allowing users to find relevant information quickly and easily.

References:
- Flask-SQLAlchemy: [https://flask-sqlalchemy.palletsprojects.com/](https://flask-sqlalchemy.palletsprojects.com/)
- SQLAlchemy-Searchable: [https://sqlalchemy-searchable.readthedocs.io/](https://sqlalchemy-searchable.readthedocs.io/)