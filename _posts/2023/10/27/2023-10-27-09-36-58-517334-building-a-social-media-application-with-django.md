---
layout: post
title: "[python] Building a social media application with Django"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

In this tutorial, we will walk through the process of building a social media application using Django, a popular Python web framework. By following this guide, you will learn how to create user authentication, implement user profiles, and allow users to post and interact with each other's content.

## Table of Contents
1. [Setting Up the project](#setting-up-the-project)
2. [User Authentication](#user-authentication)
3. [User Profiles](#user-profiles)
4. [User Posts](#user-posts)
5. [Interactions](#interactions)
6. [Conclusion](#conclusion)

## Setting Up the project
To get started, make sure you have Django installed. You can install it using pip by running the following command:

```
pip install django
```

Next, create a new Django project by running:

```
django-admin startproject social_media
```

This will create a new directory called `social_media` with the basic project structure.

## User Authentication
User authentication is an essential part of any web application. In Django, it is straightforward to set up.

First, create a new Django app for user authentication:

```
python manage.py startapp accounts
```

Next, add the `accounts` app to the `INSTALLED_APPS` list in the `settings.py` file.

Now, define the user model by creating a new file called `models.py` inside the `accounts` app directory. Here is an example of a basic user model:

```python
from django.contrib.auth.models import AbstractUser

class User(AbstractUser):
    pass
```

Next, update the `AUTH_USER_MODEL` in the `settings.py` file to point to the custom user model:

```python
AUTH_USER_MODEL = 'accounts.User'
```

Finally, run the migrations to create the necessary database tables:

```
python manage.py makemigrations
python manage.py migrate
```

## User Profiles
To add user profiles to our application, we will extend the user model.

Create a new file called `models.py` inside the `accounts` app directory and define a `Profile` model that has a one-to-one relationship with the `User` model. Here is an example:

```python
from django.db import models
from django.conf import settings

class Profile(models.Model):
    user = models.OneToOneField(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    bio = models.CharField(max_length=200)
    avatar = models.ImageField(upload_to='avatars/')

    def __str__(self):
        return self.user.username
```

Now, run the migrations:

```
python manage.py makemigrations
python manage.py migrate
```

## User Posts
Allowing users to create and view posts is a core feature of a social media application.

Create a new app called `posts`:

```
python manage.py startapp posts
```

Define a `Post` model inside the `models.py` file of the `posts` app. Here is an example:

```python
from django.db import models
from django.conf import settings

class Post(models.Model):
    author = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.content[:50]
```

Once again, run the migrations:

```
python manage.py makemigrations
python manage.py migrate
```

## Interactions
To enable users to interact with each other's content, we will implement features such as liking and commenting on posts.

Create a new app called `interactions`:

```
python manage.py startapp interactions
```

Define models for liking and commenting inside the `models.py` file of the `interactions` app. Here is an example:

```python
from django.db import models
from django.conf import settings
from posts.models import Post

class Like(models.Model):
    user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    post = models.ForeignKey(Post, on_delete=models.CASCADE)

class Comment(models.Model):
    user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    post = models.ForeignKey(Post, on_delete=models.CASCADE)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
```

Once again, run the migrations:

```
python manage.py makemigrations
python manage.py migrate
```

## Conclusion
By following this tutorial, you have learned how to build a basic social media application using Django. You now have user authentication, user profiles, user posts, and interaction features like liking and commenting.

Feel free to extend this application by adding more features, such as follow functionality or a news feed.

References:
- Django documentation: [https://docs.djangoproject.com/](https://docs.djangoproject.com/)
- Django authentication: [https://docs.djangoproject.com/en/3.2/topics/auth/](https://docs.djangoproject.com/en/3.2/topics/auth/)
- Django models: [https://docs.djangoproject.com/en/3.2/topics/db/models/](https://docs.djangoproject.com/en/3.2/topics/db/models/)

Happy coding!