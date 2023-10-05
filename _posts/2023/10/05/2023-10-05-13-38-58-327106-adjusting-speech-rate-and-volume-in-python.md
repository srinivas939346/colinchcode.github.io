---
layout: post
title: "[python] Adjusting speech rate and volume in Python"
description: " "
date: 2023-10-05
tags: [python]
comments: true
share: true
---

In this tutorial, we will explore how to adjust the speech rate and volume of a text-to-speech (TTS) output using Python. TTS technology allows us to convert written text into spoken words, and by fine-tuning the parameters such as speech rate and volume, we can create a more customized and natural-sounding voice output.

Before we get started, make sure you have the following requirements:

- Python 3.x installed on your system
- `pyttsx3` library installed (`pip install pyttsx3`)

## Adjusting Speech Rate

To adjust the speech rate, we will be using the `pyttsx3` library, which provides a cross-platform Python interface to the text-to-speech engines. The default speech rate is 200 words per minute.

```python
import pyttsx3

engine = pyttsx3.init()
rate = engine.getProperty('rate')  # Get the current speech rate
engine.setProperty('rate', rate-50)  # Decrease the speech rate by 50%
```

In the above code snippet, we first initialize the `pyttsx3` engine. Then, we use the `getProperty()` method to retrieve the current speech rate and store it in the `rate` variable. Lastly, we use the `setProperty()` method to decrease the speech rate by 50%.

## Adjusting Speech Volume

To adjust the speech volume, we can modify the `volume` property of the `pyttsx3` engine. The volume property accepts values between 0 and 1, where 0 is muted and 1 is the maximum volume.

```python
import pyttsx3

engine = pyttsx3.init()
volume = engine.getProperty('volume')  # Get the current volume
engine.setProperty('volume', volume-0.2)  # Decrease the volume by 20%
```

In the code snippet above, we first initialize the `pyttsx3` engine. Then, we use the `getProperty()` method to retrieve the current volume value and store it in the `volume` variable. Lastly, we use the `setProperty()` method to decrease the volume by 20%.

## Testing the Adjusted Speech Output

Now that we have adjusted the speech rate and volume, let's test the modified TTS output.

```python
import pyttsx3

engine = pyttsx3.init()
engine.say("Hello, world!")  # Adjusted speech output
engine.runAndWait()
```

In the code snippet above, we initialize the `pyttsx3` engine, use the `say()` method to set the text to be spoken, and then call the `runAndWait()` method to play the speech output.

## Conclusion

By adjusting the speech rate and volume parameters using the `pyttsx3` library in Python, we can easily customize the TTS output, making it more natural and personalized. Experiment with different speech rates and volumes to achieve the desired effect in your applications. Happy coding!