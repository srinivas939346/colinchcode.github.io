---
layout: post
title: "[python] Installing text-to-speech libraries in Python"
description: " "
date: 2023-10-05
tags: [python]
comments: true
share: true
---

Text-to-speech (TTS) is a technology that converts written text into spoken words. Python provides various libraries that facilitate integrating TTS functionality into your applications. In this blog post, we will explore two popular libraries: pyttsx3 and gTTS.

## Table of Contents
- [Introduction](#introduction)
- [Installing pyttsx3](#installing-pyttsx3)
- [Using pyttsx3](#using-pyttsx3)
- [Installing gTTS](#installing-gtts)
- [Using gTTS](#using-gtts)
- [Conclusion](#conclusion)

## Introduction
Text-to-speech technology can be beneficial in a wide range of applications, including accessibility features, voice assistants, narration, and more. Python offers several libraries that simplify the integration of TTS functionality into your projects. 

## Installing pyttsx3
The first library we'll explore is pyttsx3. It is a powerful TTS library that works offline and supports multiple operating systems. To install pyttsx3, you can use pip, the package installer for Python. Open your terminal or command prompt and run the following command:

```bash
pip install pyttsx3
```

## Using pyttsx3
Once you have installed pyttsx3, let's dive into an example of using it to convert text to speech. 

```python
import pyttsx3

engine = pyttsx3.init()
engine.say("Hello, world!")
engine.runAndWait()
```

In the above code snippet, we import the pyttsx3 library and initialize the TTS engine. We then use the `say` method to provide the text we want to convert to speech and the `runAndWait` method to play the speech output.

## Installing gTTS
The second library we'll explore is gTTS (Google Text-to-Speech). It is a Python library and CLI tool that uses Google Text-to-Speech API to convert text to speech. To install gTTS, use pip:

```bash
pip install gTTS
```

## Using gTTS
After installing gTTS, let's see how we can utilize it to convert text into speech.

```python
from gtts import gTTS

text = "Hello, world!"
tts = gTTS(text=text, lang='en')
tts.save("output.mp3")
```

In the code snippet above, we import the gTTS library and create a new gTTS object by passing the text and language as parameters. We then save the speech output to an MP3 file using the `save` method.

## Conclusion
In this blog post, we explored two popular libraries, pyttsx3 and gTTS, for adding text-to-speech functionality to your Python applications. We discussed how to install these libraries and provided examples of how to use them to convert text into speech. With these libraries, you can enhance the accessibility and user experience of your projects.