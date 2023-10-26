---
layout: post
title: "[python] Handling file uploads with Flask-SQLAlchemy and Flask-Uploads"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When developing a web application, handling file uploads is often a common requirement. In this tutorial, we will explore how to handle file uploads using Flask-SQLAlchemy and Flask-Uploads, two popular libraries in the Python Flask ecosystem.

## Table of Contents
- [Introduction](#introduction)
- [Setting Up the Project](#setting-up-the-project)
- [Creating the Database Model](#creating-the-database-model)
- [Configuring Flask-Uploads](#configuring-flask-uploads)
- [Uploading Files](#uploading-files)
- [Conclusion](#conclusion)

## Introduction

Flask-SQLAlchemy is a Flask extension that makes it easy to use SQLAlchemy, a powerful Object-Relational Mapping (ORM) library, with Flask. Flask-Uploads, on the other hand, is a Flask extension that simplifies handling file uploads.

By combining these two libraries, we can easily handle file uploads and associate them with our SQLAlchemy database models.

## Setting Up the Project

To get started, we first need to create a new Flask project and install the required libraries. We can use the following commands to set up the project:

```shell
$ mkdir flask-file-uploads
$ cd flask-file-uploads
$ virtualenv venv
$ source venv/bin/activate
$ pip install Flask Flask-SQLAlchemy Flask-Uploads
```

Once the project is set up, we can proceed with creating the necessary files and directories.

## Creating the Database Model

Let's start by creating a simple database model using SQLAlchemy. We will define a `File` model that will have a filename and a path to the uploaded file.

Create a new file `models.py` and add the following code:

```python
from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()

class File(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    filename = db.Column(db.String(255), nullable=False)
    path = db.Column(db.String(255), nullable=False)
```

The above code sets up a basic SQLAlchemy model with two attributes - `filename` and `path`. 

## Configuring Flask-Uploads

To use Flask-Uploads, we need to configure it in our Flask application. Create a new file `config.py` and add the following code:

```python
UPLOADED_FILES_DEST = 'uploads'
```

The above code sets the destination directory for uploaded files to `uploads`.

Next, modify the `app.py` file to load the configuration from the `config.py` file:

```python
from flask import Flask
from config import UPLOADED_FILES_DEST
from models import db

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///app.db'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
app.config['UPLOADED_FILES_DEST'] = UPLOADED_FILES_DEST

db.init_app(app)
```

The above code sets the database URI and tracks modifications to the database. Additionally, it sets the destination directory for uploaded files.

## Uploading Files

We are now ready to handle file uploads. In the `app.py` file, add the following code to handle the file upload route:

```python
from flask_uploads import UploadSet, configure_uploads, IMAGES

photos = UploadSet('photos', IMAGES)

configure_uploads(app, photos)

@app.route('/upload', methods=['POST'])
def upload():
    if 'photo' in request.files:
        filename = photos.save(request.files['photo'])
        path = photos.path(filename)
        file = File(filename=filename, path=path)
        db.session.add(file)
        db.session.commit()
        return 'File uploaded successfully.'

    return 'No file uploaded.'

@app.route('/file/<int:id>')
def file(id):
    file = File.query.get(id)
    return send_file(file.path)
```

In the above code, we first create an `UploadSet` called `photos` to handle image uploads. We then configure the uploads to use this `UploadSet`. 

The `/upload` route handles the file upload request. It saves the uploaded file, creates a new `File` object with the filename and path, and adds it to the database.

The `/file/<int:id>` route retrieves the file path from the database and sends the file as a response.

## Conclusion

In this tutorial, we explored how to handle file uploads using Flask-SQLAlchemy and Flask-Uploads. We set up the project, created a database model, configured Flask-Uploads, and implemented file upload and retrieval routes.

Handling file uploads is now significantly easier with these powerful Flask extensions. By incorporating Flask-SQLAlchemy and Flask-Uploads into your Flask applications, you can efficiently manage file uploads and associate them with your database models.

References:
- [Flask-SQLAlchemy Documentation](https://flask-sqlalchemy.palletsprojects.com/)
- [Flask-Uploads Documentation](https://pythonhosted.org/Flask-Uploads/)