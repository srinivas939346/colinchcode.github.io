---
layout: post
title: "[python] Encrypting and hashing user passwords in Flask-SQLAlchemy"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

User password security is of utmost importance in any application. Storing passwords in plain text is a huge security risk, as it makes them vulnerable to unauthorized access. In this blog post, we will explore how to encrypt and hash user passwords in Flask-SQLAlchemy, a popular Python web development framework.

## Table of Contents
- [What is Flask-SQLAlchemy?](#what-is-flask-sqlalchemy)
- [Why Encrypt and Hash Passwords?](#why-encrypt-and-hash-passwords)
- [Encrypting Passwords in Flask-SQLAlchemy](#encrypting-passwords-in-flask-sqlalchemy)
- [Hashing Passwords in Flask-SQLAlchemy](#hashing-passwords-in-flask-sqlalchemy)
- [Conclusion](#conclusion)

## What is Flask-SQLAlchemy?

Flask-SQLAlchemy is a Flask extension that integrates SQLAlchemy, a powerful database toolkit for Python, with Flask, a lightweight web framework. It provides a convenient way to interact with databases and perform various operations, including storing and retrieving user information.

## Why Encrypt and Hash Passwords?

When storing user passwords in a database, it is crucial to ensure their security. Encryption is the process of converting plain text into a form that is not easily readable without a decryption key. Hashing, on the other hand, is a one-way process of generating a fixed-length value from input data.

By encrypting and hashing passwords, we can protect them from unauthorized access, even if the database is compromised. When a user logs in, their password can be hashed again and compared with the stored hash to verify its correctness.

## Encrypting Passwords in Flask-SQLAlchemy

To encrypt passwords in Flask-SQLAlchemy, we can use a password-based key derivation function (PBKDF) like bcrypt. PBKDFs are specifically designed for password hashing and provide additional security measures like salting to prevent rainbow table attacks.

Here's an example of how to encrypt passwords using bcrypt in Flask-SQLAlchemy:

```python
import bcrypt

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(50), unique=True, nullable=False)
    password = db.Column(db.String(100), nullable=False)

    def set_password(self, password):
        hashed_password = bcrypt.hashpw(password.encode('utf-8'), bcrypt.gensalt())
        self.password = hashed_password.decode('utf-8')
    
    def check_password(self, password):
        return bcrypt.checkpw(password.encode('utf-8'), self.password.encode('utf-8'))
```

In the above example, we import the `bcrypt` library and add two methods to the `User` model: `set_password` and `check_password`. 
- The `set_password` method generates a hashed password using the `bcrypt.hashpw` function and stores it in the `password` field. 
- The `check_password` method compares the hashed password with the provided password using `bcrypt.checkpw` and returns the result.

## Hashing Passwords in Flask-SQLAlchemy

Flask-SQLAlchemy also provides a way to hash passwords using a different library called `passlib`. Passlib supports various hashing algorithms like SHA512, bcrypt, and scrypt.

Here's an example of how to hash passwords using `passlib` in Flask-SQLAlchemy:

```python
from passlib.hash import sha256_crypt

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(50), unique=True, nullable=False)
    password = db.Column(db.String(100), nullable=False)

    def set_password(self, password):
        hashed_password = sha256_crypt.hash(password)
        self.password = hashed_password
    
    def check_password(self, password):
        return sha256_crypt.verify(password, self.password)
```

In the above example, we import the `sha256_crypt` algorithm from `passlib.hash` and use it to hash and verify passwords. 
- The `set_password` method generates a hashed password using `sha256_crypt.hash` and stores it in the `password` field. 
- The `check_password` method compares the hashed password with the provided password using `sha256_crypt.verify` and returns the result.

## Conclusion

Securing user passwords is of utmost importance in any application. By encrypting and hashing passwords, we can protect them from unauthorized access in case of a data breach. In this blog post, we explored how to encrypt and hash passwords in Flask-SQLAlchemy using libraries like bcrypt and passlib. By implementing these techniques, you can enhance the security of your Flask web applications.