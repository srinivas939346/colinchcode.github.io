---
layout: post
title: "[python] Building a simple interactive text-to-speech program in Python"
description: " "
date: 2023-10-05
tags: [python]
comments: true
share: true
---

In this tutorial, we will build a simple text-to-speech program using Python. This program will allow users to input text, read it aloud using the text-to-speech conversion, and adjust the speech rate.

## Table of Contents
- [Introduction](#introduction)
- [Setting Up](#setting-up)
- [Installing Dependencies](#installing-dependencies)
- [Building the Text-to-Speech Program](#building-the-text-to-speech-program)
- [Conclusion](#conclusion)

## Introduction
Text-to-speech (TTS) is a technology that converts written text into spoken words. It can be a useful feature in various applications, such as voice assistants, audiobooks, and accessibility tools. Python provides libraries that make it easy to implement a text-to-speech functionality in our programs.

In this tutorial, we will use the `pyttsx3` library, which is a cross-platform text-to-speech library for Python. It supports multiple TTS engines, allowing us to choose the one that best suits our needs.

## Setting Up
Before we get started, make sure you have Python installed on your computer. You can download Python from the official Python website, [python.org](https://www.python.org). Once Python is installed, open your terminal or command prompt and follow the steps below.

## Installing Dependencies
To use the `pyttsx3` library, we need to install it first. Open your terminal or command prompt and run the following command:

```python
pip install pyttsx3
```

This command will install the `pyttsx3` library along with any required dependencies.

## Building the Text-to-Speech Program
Now let's start building our text-to-speech program. Create a new Python file and import the `pyttsx3` library:

```python
import pyttsx3
```

Next, initialize the text-to-speech engine:

```python
engine = pyttsx3.init()
```

To allow the user to input text, we can use the `input()` function:

```python
text = input("Enter the text to be spoken: ")
```

Now, we can set the speech rate (default is 200 words per minute) using the `setProperty()` method:

```python
rate = engine.getProperty('rate')
engine.setProperty('rate', rate - 50)
```

Finally, we can use the `say()` method to speak the input text:

```python
engine.say(text)
engine.runAndWait()
```

Save the file and run the program. You will be prompted to enter the text you want to hear. After entering the text, the program will convert it to speech and speak it aloud.

You can experiment with different speech rates by adjusting the value passed to `setProperty()`. Higher values will increase the speech rate, while lower values will decrease it.

## Conclusion
In this tutorial, we built a simple text-to-speech program using Python and the `pyttsx3` library. We learned how to install the library, initialize the TTS engine, allow user input, and adjust the speech rate. Feel free to explore the capabilities of the `pyttsx3` library and expand the functionality of your program.