---
layout: post
title: "[python] Implementing user feedback and rating system in Web2py"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Web2py is a Python web framework that allows you to easily build and deploy web applications. In this blog post, we will walk through the process of implementing a user feedback and rating system in a Web2py application.

### Table of Contents
- [Setting Up the Database](#setting-up-the-database)
- [Creating Models](#creating-models)
- [Designing the User Interface](#designing-the-user-interface)
- [Implementing Feedback](#implementing-feedback)
- [Implementing Rating](#implementing-rating)
- [Conclusion](#conclusion)

### Setting Up the Database

First, let's set up the database for our application. We will need a table to store user feedback and another table to store user ratings. Here's an example of how you can define these tables in Web2py's database model:

```python
db.define_table('feedback',
    Field('user_id', 'reference auth_user', default=auth.user_id),
    Field('content', 'text'),
    Field('timestamp', 'datetime', default=request.now)
)

db.define_table('rating',
    Field('user_id', 'reference auth_user', default=auth.user_id),
    Field('rating', 'integer', requires=IS_IN_SET(range(1, 6))),
    Field('timestamp', 'datetime', default=request.now)
)
```

### Creating Models

Next, we need to create models for the feedback and rating tables. In your `models.py`, add the following code:

```python
from gluon.tools import Auth

auth = Auth(db)
auth.define_tables()

db.feedback.user_id.writable = db.feedback.user_id.readable = False
db.rating.user_id.writable = db.rating.user_id.readable = False
```

This code sets up the authentication module and makes the `user_id` field read-only so that users can't manipulate it.

### Designing the User Interface

Now that we have our tables and models set up, let's design the user interface to collect user feedback and display ratings. You can create a form to collect feedback using Web2py's `SQLFORM` helper. Here's an example:

```python
def feedback():
    form = SQLFORM(db.feedback)

    if form.process().accepted:
        response.flash = 'Thank you for your feedback!'

    return dict(form=form)
```

To display ratings, you can create a view that fetches the average rating from the database and renders it on the page:

```python
def rating():
    average_rating = db.rating.rating.avg()
    count = db.rating.rating.count()

    return dict(average_rating=average_rating, count=count)
```

### Implementing Feedback

In the previous section, we created a form to collect user feedback. To ensure that only authenticated users can submit feedback, we can add the `auth.requires_login()` decorator to the `feedback()` function.

```python
@auth.requires_login()
def feedback():
    form = SQLFORM(db.feedback)

    if form.process().accepted:
        response.flash = 'Thank you for your feedback!'

    return dict(form=form)
```

### Implementing Rating

To implement the rating system, first, we need to create a form with rating options (e.g., 1 to 5 stars). Here's an example:

```python
def rate():
    form = SQLFORM.factory(
        Field('rating', 'integer', requires=IS_IN_SET(range(1, 6))),
        submit_button='Rate'
    )

    if form.process().accepted:
        db.rating.insert(rating=form.vars.rating)
        response.flash = 'Thank you for rating!'

    return dict(form=form)
```

To prevent users from rating multiple times, we can add a condition to check if the user has already rated:

```python
@auth.requires_login()
def rate():
    user_id = auth.user_id

    rating = db.rating(rating.user_id == user_id)
    if rating:
        response.flash = 'You have already rated!'
        form = None
    else:
        form = SQLFORM.factory(
            Field('rating', 'integer', requires=IS_IN_SET(range(1, 6))),
            submit_button='Rate'
        )

        if form.process().accepted:
            db.rating.insert(rating=form.vars.rating)
            response.flash = 'Thank you for rating!'

    return dict(form=form)
```

### Conclusion

In this blog post, we walked through the process of implementing a user feedback and rating system in a Web2py application. We learned how to set up the database, create models, design the user interface, and implement feedback and rating functionalities. With this system in place, you can collect valuable feedback from your users and utilize their ratings to enhance your web application's user experience.