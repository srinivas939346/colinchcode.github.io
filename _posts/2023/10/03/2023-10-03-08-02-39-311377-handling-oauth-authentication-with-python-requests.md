---
layout: post
title: "[python] Handling OAuth authentication with Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

OAuth authentication is widely used in modern web applications to authenticate and authorize users. In this blog post, we will explore how to handle OAuth authentication using the Python Requests library.

## Table of Contents
1. [What is OAuth?](#what-is-oauth)
2. [Installing Requests library](#installing-requests-library)
3. [OAuth Flow](#oauth-flow)
4. [Getting an Access Token](#getting-an-access-token)
5. [Making Authenticated Requests](#making-authenticated-requests)
6. [Conclusion](#conclusion)

## What is OAuth?
OAuth (Open Authorization) is an open standard for authentication and authorization used by apps to access user resources on other websites without sharing their credentials. It provides a secure way for users to grant permissions to third-party applications to access their data.

## Installing Requests library
Before we proceed, let's make sure we have the Requests library installed. If you don't have it, you can install it using pip:

```shell
pip install requests
```

## OAuth Flow
The OAuth flow consists of several steps that involve the client application, server application, and the user. Here is a simplified version of the flow:

1. The client application sends a request to the server application for authorization.
2. The server application generates an authorization URL and redirects the user to that URL.
3. The user authenticates with the service provider and grants the requested permissions.
4. The service provider redirects the user back to the client application with a temporary authorization code.
5. The client application sends a request to the server application to exchange the authorization code for an access token.
6. The server application validates the authorization code and exchanges it for an access token.
7. The server application returns the access token to the client application.
8. The client application can now use the access token to make authenticated requests on behalf of the user.

## Getting an Access Token
To get an access token, you need to follow the OAuth flow specific to the service you are integrating with. Each service provider may have its own endpoints and parameters for authentication. For example, let's consider the GitHub API authentication flow:

1. Register a new OAuth application on GitHub.
2. Retrieve the client ID and client secret provided by GitHub.
3. Redirect the user to the GitHub authorization URL with the required parameters.
4. Once the user grants the permissions, GitHub redirects the user back to a callback URL specified in your application.
5. Exchange the authorization code received from GitHub for an access token.
6. Use the access token to make authenticated requests to the GitHub API.

Here is an example of obtaining an access token from GitHub using Python Requests:

```python
import requests

# Define the GitHub OAuth endpoints and client credentials
authorize_url = 'https://github.com/login/oauth/authorize'
token_url = 'https://github.com/login/oauth/access_token'
client_id = 'YOUR_CLIENT_ID'
client_secret = 'YOUR_CLIENT_SECRET'

# Redirect the user to the GitHub authorization URL
authorization_redirect_url = authorize_url + '?client_id=' + client_id
print('Please go to the following URL and authorize the application:')
print(authorization_redirect_url)

# Receiving the authorization code
authorization_code = input('Enter the authorization code: ')

# Exchange the authorization code for an access token
token_payload = {
    'client_id': client_id,
    'client_secret': client_secret,
    'code': authorization_code
}
token_response = requests.post(token_url, data=token_payload)

# Parse the access token from the response
access_token = token_response.json()['access_token']

print('Access token:', access_token)
```

## Making Authenticated Requests
Once you have obtained an access token, you can include it in your requests to authenticate with the API. Most APIs expect the access token to be sent in the Authorization header using the Bearer authentication scheme. Here is an example of making an authenticated request to the GitHub API:

```python
import requests

url = 'https://api.github.com/user'
headers = {
    'Authorization': f'Bearer {access_token}'
}

response = requests.get(url, headers=headers)
print(response.json())
```

## Conclusion
Handling OAuth authentication with Python Requests library is relatively straightforward. By following the OAuth flow specific to the service provider and using the client credentials and access token, you can authenticate and make requests on behalf of the user. Remember to handle any error scenarios and implement proper security practices when dealing with user authentication.

Happy coding!