---
layout: post
title: "[python] Saving the generated speech as an audio file in Python"
description: " "
date: 2023-10-05
tags: [python]
comments: true
share: true
---

In this tutorial, we'll explore how to save a generated speech as an audio file using Python. We'll be utilizing a Python library called `pyttsx3` which provides cross-platform support for text-to-speech conversion.

## Table of Contents

1. [Installing pyttsx3](#installing-pyttsx3)
2. [Generating Speech](#generating-speech)
3. [Saving Speech as Audio](#saving-speech-as-audio)
4. [Conclusion](#conclusion)

## 1. Installing pyttsx3

First, we need to install the `pyttsx3` library. You can use `pip` to install it by running the following command:

```
pip install pyttsx3
```

## 2. Generating Speech

Let's start by generating speech from a given text. Here's an example:

```python
import pyttsx3

# Initialize the speech engine
engine = pyttsx3.init()

# Set the speech rate (optional)
engine.setProperty('rate', 150)

# Set the voice (optional)
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[1].id)  # selecting the second voice 

# Provide the text to be spoken
text = "Hello, this is a sample text. It will be converted to speech."

# Speak the text
engine.say(text)
engine.runAndWait()
```

In the above code, we initialize the speech engine using the `init()` function from `pyttsx3` library. We can set the speech rate or select a specific voice using the `setProperty()` function. Then, we provide the text to be spoken using the `say()` function and use `runAndWait()` to wait until the speech is completed.

## 3. Saving Speech as Audio

To save the generated speech as an audio file, we'll use the `pyttsx3` engine to save it in the WAV format. Here's an example:

```python
import pyttsx3

# Initialize the speech engine
engine = pyttsx3.init()

# Set the speech rate (optional)
engine.setProperty('rate', 150)

# Set the voice (optional)
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[1].id)  # selecting the second voice 

# Provide the text to be spoken
text = "Hello, this is a sample text. It will be converted to speech."

# Set the output file path
output_path = "speech.wav"

# Save the speech as audio
engine.save_to_file(text, output_path)
engine.runAndWait()
```

In the above code, we use the `save_to_file()` function to save the speech as an audio file. We provide the text to be spoken and the output file path as arguments. In this example, the speech would be saved as `speech.wav`.

## 4. Conclusion

In this tutorial, we explored how to save the generated speech as an audio file using the `pyttsx3` library in Python. Now you can integrate text-to-speech functionality into your Python applications and save the generated speech as audio for future use.