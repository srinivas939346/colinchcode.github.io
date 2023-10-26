---
layout: post
title: "[python] Applying equalization to audio with Pydub"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Equalization is a technique used to adjust the frequency response of an audio signal. It allows us to boost or attenuate specific frequencies to achieve the desired sound. In this blog post, we will explore how to apply equalization to audio using PyDub, a simple and easy-to-use library for audio processing in Python.

### Installing PyDub

Before we begin, make sure you have PyDub installed. You can install it by running the following command:

```python
pip install pydub
```

### Loading an Audio File

First, we need to load an audio file that we want to equalize. PyDub supports various audio file formats such as MP3, WAV, and more. Let's assume we have an audio file called "sample.mp3". Here's how you can load it using PyDub:

```python
from pydub import AudioSegment

audio = AudioSegment.from_file("sample.mp3")
```

### Applying Equalization

To apply equalization, PyDub provides a method called `equalize()`. This method allows us to define the desired equalization curve using a list of gain values for different frequencies.

```python
equalized_audio = audio.equalize([0, 3, 0, -2, 0, 0, 0, 5, 0, 0, 0])
```

In the example above, we are providing a gain value of 3dB for the second frequency band and -2dB for the fourth frequency band. Other frequency bands are set to 0dB, indicating no gain or attenuation.

### Exporting the Equalized Audio

Once the equalization is applied, we can export the equalized audio to a desired file format, such as WAV or MP3. Here's an example of exporting the equalized audio to a WAV file:

```python
equalized_audio.export("equalized_sample.wav", format="wav")
```

### Full Example

Here's the complete example of applying equalization to an audio file using PyDub:

```python
from pydub import AudioSegment

audio = AudioSegment.from_file("sample.mp3")

equalized_audio = audio.equalize([0, 3, 0, -2, 0, 0, 0, 5, 0, 0, 0])

equalized_audio.export("equalized_sample.wav", format="wav")
```

### Conclusion

Equalization is a powerful technique that allows us to shape the audio signal to our liking. In this blog post, we explored how to apply equalization to an audio file using PyDub. By adjusting the gain values for different frequency bands, we can achieve the desired sound. PyDub makes it easy to perform audio processing tasks in Python, and equalization is just one of many capabilities it offers.

To learn more about PyDub and its functionalities, you can refer to the [official documentation](https://pydub.com/).