---
layout: post
title: "[python] Building user authentication in Django"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Authentication is a critical feature in web applications that ensures only authorized users can access certain resources or perform specific actions. In this tutorial, we will walk through the process of building user authentication in Django, a popular web framework for Python.

## Table of Contents
1. [Introduction](#introduction)
2. [Setting up Django](#setting-up-django)
3. [Creating the User Model](#creating-the-user-model)
4. [Registration](#registration)
5. [Login](#login)
6. [Logout](#logout)
7. [Conclusion](#conclusion)

## Introduction
User authentication involves managing user accounts, registration, login, and logout functionality. Django provides a built-in authentication system that simplifies these tasks, saving developers valuable time.

## Setting up Django
To get started, make sure you have Django installed. You can install Django using pip, the Python package manager. Open your terminal or command prompt and run the following command:

```
pip install django
```

Once Django is installed, create a new Django project using the following command:

```
django-admin startproject myproject
```

Navigate to the project directory by running:

```
cd myproject
```

## Creating the User Model
Django provides a default User model, but we can also create a custom user model to include additional fields or modify existing ones. To create a custom user model, follow these steps:

1. Open the `models.py` file in your Django app directory.
2. Import the required modules by adding the following lines at the top of the file:

```python
from django.db import models
from django.contrib.auth.models import AbstractBaseUser, BaseUserManager, PermissionsMixin
```

3. Create a custom user manager by subclassing `BaseUserManager` and overriding the necessary methods. This manager will handle the creation and management of user accounts.

```python
class UserManager(BaseUserManager):
    def create_user(self, email, password=None, **extra_fields):
        # Implement the logic to create a user
        pass
        
    def create_superuser(self, email, password=None, **extra_fields):
        # Implement the logic to create a superuser
        pass
```

4. Define the custom user model and its fields by subclassing `AbstractBaseUser` and `PermissionsMixin`. Use the custom user manager created earlier.

```python
class User(AbstractBaseUser, PermissionsMixin):
    email = models.EmailField(unique=True)
    # Add additional fields as required
    # ...

    objects = UserManager()
    
    USERNAME_FIELD = 'email'
    # Add additional fields to REQUIRED_FIELDS as needed
    # ...
```

5. Finally, update the `AUTH_USER_MODEL` setting in your Django project's `settings.py` file to use the custom user model.

```python
AUTH_USER_MODEL = 'your_app.User'
```

## Registration
Implementing user registration involves creating a registration form and view. Here's a simplified example:

1. Create a new file called `forms.py` in your Django app directory.
2. Create a registration form by subclassing `forms.ModelForm` and specifying the required fields.

```python
from django import forms
from .models import User

class RegistrationForm(forms.ModelForm):
    password = forms.CharField(widget=forms.PasswordInput)
    
    class Meta:
        model = User
        fields = ['email', 'password']
```

3. Create a registration view to handle form submission, validate the data, and create a new user account.

```python
from django.shortcuts import render, redirect
from .forms import RegistrationForm

def register(request):
    if request.method == 'POST':
        form = RegistrationForm(request.POST)
        
        if form.is_valid():
            form.save()
            return redirect('login')
    else:
        form = RegistrationForm()
    
    return render(request, 'registration.html', {'form': form})
```

4. Create a registration template (`registration.html`) in the app's `templates` directory to display the registration form.

```html
{% raw %}
{% extends 'base.html' %}

{% block content %}
  <h2>Registration</h2>
  <form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Register</button>
  </form>
{% endblock %}
{% endraw %}
```

## Login
To implement user login functionality, follow these steps:

1. Create a login form by subclassing `forms.Form` and specifying the required fields.

```python
from django import forms

class LoginForm(forms.Form):
    email = forms.EmailField()
    password = forms.CharField(widget=forms.PasswordInput)
```

2. Create a login view to handle form submission, authenticate the user, and log them in.

```python
from django.shortcuts import render, redirect
from django.contrib.auth import authenticate, login
from .forms import LoginForm

def user_login(request):
    if request.method == 'POST':
        form = LoginForm(request.POST)
        
        if form.is_valid():
            email = form.cleaned_data['email']
            password = form.cleaned_data['password']
            user = authenticate(request, email=email, password=password)
            
            if user is not None:
                login(request, user)
                return redirect('dashboard')
            else:
                form.add_error(None, 'Invalid login credentials')
    else:
        form = LoginForm()
    
    return render(request, 'login.html', {'form': form})
```

3. Create a login template (`login.html`) in the app's `templates` directory to display the login form.

```html
{% raw %}
{% extends 'base.html' %}

{% block content %}
  <h2>Login</h2>
  <form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Login</button>
  </form>
{% endblock %}
{% endraw %}
```

## Logout
Implementing user logout functionality is straightforward in Django. Follow these steps:

1. Create a logout view to handle the logout process.

```python
from django.shortcuts import redirect
from django.contrib.auth import logout

def user_logout(request):
    logout(request)
    return redirect('login')
```

2. Create a logout link or button in your templates to trigger the logout view.

```html
<a href="{% url 'logout' %}">Logout</a>
```

## Conclusion
Congratulations! You have learned how to build user authentication in Django. This tutorial covered creating a custom user model, implementing registration and login functionality, and enabling user logout. With Django's built-in authentication system, you can easily enhance your web applications with secure user management.