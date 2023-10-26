---
layout: post
title: "[python] Uploading files to the database with SQLAlchemy in Flask"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When working with web applications, file uploading is a common feature that allows users to upload images, documents, or other types of files to the server. In a Flask application, you can use SQLAlchemy, a powerful Object-Relational Mapper (ORM), to handle file uploads and store them in the database.

In this tutorial, we will go through the process of setting up file uploading with SQLAlchemy in a Flask application.

## Prerequisites

Before we begin, make sure you have the following installed:

- Flask
- SQLAlchemy

You can install these dependencies using pip:

```bash
pip install flask
pip install sqlalchemy
```

## Setting up the Flask Application

First, let's create a basic Flask application that will serve as the foundation for our file uploading functionality. Create a new Python file called `app.py` and add the following code:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run()
```

Save the file and run it by executing `python app.py` in the terminal. You should see the "Hello, World!" message when you visit `http://localhost:5000` in your browser.

## Creating the File Upload Form

Next, let's create a simple HTML form that allows users to upload a file. In the `home` route, modify the code to return an HTML template with the file upload form:

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def home():
    return render_template('index.html')

if __name__ == '__main__':
    app.run()
```

Create a new folder called `templates` in the same directory as your `app.py` file, and inside the `templates` folder, create a new file named `index.html`. Add the following code to the `index.html` file:

```html
{% raw %}
<!DOCTYPE html>
<html>
<head>
    <title>File Upload</title>
</head>
<body>
    <h1>File Upload</h1>
    <form action="{{ url_for('upload') }}" method="POST" enctype="multipart/form-data">
        <input type="file" name="file">
        <input type="submit" value="Upload">
    </form>
</body>
</html>
{% endraw %}
```
{% raw %}
This form contains a file input field and a submit button. The form's `action` attribute is set to `{{ url_for('upload') }}`, which will be the route responsible for handling the file upload.
{% endraw %}
## Handling the File Upload

Now, let's modify the Flask app to handle the file upload. Import the `request` module from Flask and add a new route for the `/upload` URL:

```python
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route('/')
def home():
    return render_template('index.html')

@app.route('/upload', methods=['POST'])
def upload():
    file = request.files['file']
    # Code to store the file in the database using SQLAlchemy

if __name__ == '__main__':
    app.run()
```

In the `upload` route, we use `request.files` to access the uploaded file. We can then store it in the database using SQLAlchemy.

## Storing the File in the Database

To store the uploaded file in the database, we will create a model using SQLAlchemy. Add the following code to your `app.py` file:

```python
from flask import Flask, render_template, request
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///uploads.db'  # Replace with your database connection string
db = SQLAlchemy(app)

class File(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(100))

@app.route('/')
def home():
    return render_template('index.html')

@app.route('/upload', methods=['POST'])
def upload():
    file = request.files['file']
    new_file = File(name=file.filename)
    db.session.add(new_file)
    db.session.commit()

    return 'File uploaded successfully!'

if __name__ == '__main__':
    app.run()
```

In this code, we define a `File` model with an `id` and `name` field. In the `upload` route, we create a new `File` object and save the file name. We then add the object to the session and commit the changes to the database.

## Conclusion

Congratulations! You have successfully set up file uploading with SQLAlchemy in a Flask application. Users can now upload files, and they will be stored in the database.

Keep in mind that storing files in a database may not be the best approach for all use cases. Depending on your requirements, you may want to consider storing files on disk or using cloud storage solutions like AWS S3.

For more information on Flask and SQLAlchemy, refer to the official documentation links below:

- Flask: [https://flask.palletsprojects.com/](https://flask.palletsprojects.com/)
- SQLAlchemy: [https://www.sqlalchemy.org/](https://www.sqlalchemy.org/)

Happy coding!