---
layout: post
title: "[python] Creating a new Web2py project"
description: " "
date: 2023-10-27
tags: [python]
comments: true
share: true
---

Web2py is a free, open-source web application framework written in Python. It is designed to simplify web development by providing a comprehensive set of tools and features. In this tutorial, we will walk through the steps to create a new Web2py project.

## Prerequisites

Before getting started, make sure you have the following prerequisites installed on your machine:

- Python (version 2.7 or 3.x)
- pip (Python package manager)

## Step 1: Install Web2py

The first step is to install Web2py. Open a terminal or command prompt and run the following command:

```shell
pip install web2py
```

Alternatively, you can visit the official Web2py website at [http://www.web2py.com/init/default/download](http://www.web2py.com/init/default/download) and download the installation package suitable for your operating system.

## Step 2: Create a new project

Once Web2py is installed, navigate to the directory where you want to create your new project. In the terminal or command prompt, run the following command:

```shell
web2py.py -a <admin_password> -c <project_name>
```

Replace `<admin_password>` with a custom admin password of your choice and `<project_name>` with the desired name for your project. This command will create a new Web2py project with the specified admin password and project name.

## Step 3: Start the development server

To start the Web2py development server, navigate to the project directory using the terminal or command prompt and run the following command:

```shell
python web2py.py
```

This will start the development server on the default port (8000). Open your web browser and visit [http://localhost:8000](http://localhost:8000) to see the default Web2py welcome page.

## Step 4: Explore project structure

After starting the development server, you can explore the project structure. The main files and directories in a Web2py project are:

- **applications**: Contains your web applications.
- **databases**: Stores the SQLite database.
- **controllers**: Contains the Python files that define the application logic.
- **views**: Contains HTML, CSS, and JavaScript files for rendering the user interface.
- **models**: Contains the database models.
- **modules**: Contains reusable modules or libraries.
- **static**: Stores static files like images, stylesheets, and JavaScript files.

Feel free to explore and modify these files to build your web application.

## Conclusion

In this tutorial, we have learned how to create a new Web2py project. Web2py provides an easy-to-use framework for web development. Now, you can start building your web applications using Web2py's powerful features and tools.

References:
- [Web2py official website](http://www.web2py.com/)
- [Web2py GitHub repository](https://github.com/web2py/web2py)