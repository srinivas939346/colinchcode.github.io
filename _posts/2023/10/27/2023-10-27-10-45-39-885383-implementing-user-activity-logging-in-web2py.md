---
layout: post
title: "[python] Implementing user activity logging in Web2py"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Web2py is a Python web framework that allows for rapid development of web applications. One common requirement in web applications is to log user activities for auditing, security, and troubleshooting purposes. In this blog post, we will discuss how to implement user activity logging in a Web2py application.

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Setting up the Log Table](#setting-up-the-log-table)
3. [Logging User Activities](#logging-user-activities)
4. [Viewing User Activity Logs](#viewing-user-activity-logs)

## Prerequisites <a name="prerequisites"></a>

To follow along with this tutorial, make sure you have the following:

- Web2py installed on your system
- A basic understanding of Web2py framework and Python

## Setting up the Log Table <a name="setting-up-the-log-table"></a>

First, we need to set up a database table to store the user activity logs. In Web2py, you can use the built-in database abstraction layer to define and create tables. Open the `models/db.py` file in your Web2py application and add the following code:

```python
db.define_table('activity_log',
                Field('user_id', 'reference auth_user'),
                Field('activity', 'string'),
                Field('timestamp', 'datetime', default=request.now))
```

The above code defines a table named "activity_log" with three fields: "user_id" referencing the built-in "auth_user" table, "activity" to store the log message, and "timestamp" to record the time of the logged activity.

Make sure to run the web2py setup code to create the table using:

```python
from gluon.tools import *

db = DAL()
auth = Auth(db)
auth.define_tables()

auth_development_login()
```

This will create the necessary database table for logging user activities.

## Logging User Activities <a name="logging-user-activities"></a>

Now that we have the log table set up, we can start logging user activities. In your application's controller file (e.g., `controllers/default.py`), add the following code to log user activities:

```python
def index():
    # Code for your index action goes here

    # log user activity
    db.activity_log.insert(user_id=auth.user_id,
                           activity="User visited the index page")
    return dict()

def user_profile():
    # Code for your user_profile action goes here

    # log user activity
    db.activity_log.insert(user_id=auth.user_id,
                           activity=f"User visited the user profile page for user {request.args(0)}")
    return dict()
```

In the above code, we use the `db.activity_log.insert()` method to insert new log entries into the "activity_log" table. We provide the user's ID (`auth.user_id`) and the activity description as parameters to the `insert` method.

You can add similar logging code in other actions or event handlers as needed to track user activities.

## Viewing User Activity Logs <a name="viewing-user-activity-logs"></a>

To view the user activity logs, we can add a new action in our controller file (`controllers/default.py` in this example) that queries the log table and displays the log entries. Add the following code:

```python
def view_logs():
    logs = db(db.activity_log).select()
    return dict(logs=logs)
```

In the above code, we query the "activity_log" table using the `db().select()` method and pass the result to the view. You can customize the view to display the logs in a user-friendly format.

Create a new view file `views/default/view_logs.html` and add the following code:

```html
{% raw %}
{{extend 'layout.html'}}

{{block body}}
<h1>User Activity Logs</h1>
<table>
    <tr>
        <th>User</th>
        <th>Activity</th>
        <th>Timestamp</th>
    </tr>
    {% for log in logs: %}
    <tr>
        <td>{{ log.user_id.first_name }} {{ log.user_id.last_name }}</td>
        <td>{{ log.activity }}</td>
        <td>{{ log.timestamp }}</td>
    </tr>
    {% endfor %}
</table>
{{end}}
{% endraw %}
```

This view template will render a table listing the user activity logs with columns for user, activity, and timestamp.

To access the logs, you can add a link in your application's navigation or create a separate page dedicated to viewing the logs.

That's it! You have now implemented user activity logging in your Web2py application. This will help you keep track of user activities and troubleshoot any issues that may arise.

## Conclusion

User activity logging is an important aspect of web application development. By implementing it in your Web2py application, you can ensure that you have a record of user actions for various purposes. With the steps outlined in this blog post, you can easily set up user activity logging and view the logs in your Web2py application.