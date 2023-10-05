---
layout: post
title: "[python] Changing the voice and language in Python text-to-speech"
description: " "
date: 2023-10-05
tags: [python]
comments: true
share: true
---

Text-to-speech (TTS) technology allows us to convert written text into spoken words. Python provides various libraries that make it easier to implement TTS functionality into our applications. One popular library is pyttsx3, which allows us to control the voice and language used in the generated speech.

In this tutorial, we will learn how to change the voice and language in Python text-to-speech using the pyttsx3 library.

## Table of Contents
- [Installing pyttsx3](#installing-pyttsx3)
- [Changing the Voice](#changing-the-voice)
- [Modifying the Language](#modifying-the-language)
- [Putting It All Together](#putting-it-all-together)
- [Conclusion](#conclusion)

## Installing pyttsx3

To get started, we need to install the pyttsx3 library. Open your terminal or command prompt and run the following command:

```shell
pip install pyttsx3
```

Once the installation is complete, we can start using pyttsx3 in our Python projects.

## Changing the Voice

By default, pyttsx3 uses the default system voice. However, it provides a way to change the voice to something more to our liking. Here's how you can change the voice:

```python
import pyttsx3

engine = pyttsx3.init()

# Get a list of available voices
voices = engine.getProperty('voices')

# Set the desired voice index
desired_voice_index = 1

# Set the voice using the index
engine.setProperty('voice', voices[desired_voice_index].id)

# Test the voice
engine.say("Hello, this is a test.")

# Save the changes
engine.runAndWait()
```

In the code above, we first initialize the pyttsx3 engine. We then use `engine.getProperty('voices')` to obtain a list of available voices. We can select the desired voice by using its index and set it as the current voice using `engine.setProperty('voice', voices[desired_voice_index].id)`.

After setting the voice, we can test it by using `engine.say("Hello, this is a test.")`. Finally, we save our changes using `engine.runAndWait()`.

## Modifying the Language

We can also modify the language used in the TTS output. The pyttsx3 library supports a wide range of languages. Here's an example of how to change the language:

```python
import pyttsx3

engine = pyttsx3.init()

# Set the desired language
desired_language = 'en-us'

# Set the language
engine.setProperty('language', desired_language)

# Test the modified language
engine.say("Hello, how are you?")

# Save the changes
engine.runAndWait()
```

In the code snippet above, we set the `desired_language` variable to the desired language code (e.g., 'en-us' for English US). We then use `engine.setProperty('language', desired_language)` to set the desired language. We can test the modified language by using `engine.say("Hello, how are you?")` and saving our changes with `engine.runAndWait()`.

## Putting It All Together

Now, let's see an example that combines changing the voice and modifying the language:

```python
import pyttsx3

engine = pyttsx3.init()

# Get a list of available voices
voices = engine.getProperty('voices')

# Set the desired voice index
desired_voice_index = 1

# Set the voice using the index
engine.setProperty('voice', voices[desired_voice_index].id)

# Set the desired language
desired_language = 'en-us'

# Set the language
engine.setProperty('language', desired_language)

# Test the modified voice and language
engine.say("Hello, this is a test.")

# Save the changes
engine.runAndWait()
```

In the above example, we first change the voice using the desired voice index. Next, we modify the language using the desired language code. Finally, we test the modified voice and language by using the `engine.say()` method and save the changes with `engine.runAndWait()`.

## Conclusion

In this tutorial, we have learned how to change the voice and language in Python text-to-speech using the pyttsx3 library. By using the provided methods, we can customize the TTS output to our preferences in terms of the voice and language used. Feel free to experiment and incorporate this functionality into your speech-enabled applications.