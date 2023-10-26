---
layout: post
title: "[python] Generating audio spectrograms with Pydub"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In this tutorial, we will explore how to generate audio spectrograms using the Pydub library in Python. Spectrograms are visual representations of the frequencies present in an audio signal over time, allowing us to analyze the spectral content of the audio.

### What is Pydub?

Pydub is an easy-to-use library for audio manipulation in Python. It provides a simple API for performing common audio tasks such as reading and writing audio files, cutting, concatenating, and applying effects.

### Installing Pydub

To install Pydub, you can use the following command:

```
pip install pydub
```

### Generating a spectrogram

Let's start by generating a spectrogram from an audio file. First, we need to import the necessary modules:

```python
from pydub import AudioSegment
from pydub.playback import play
import numpy as np
import matplotlib.pyplot as plt
```

Next, we can load the audio file using Pydub's `AudioSegment` class:

```python
audio = AudioSegment.from_file("audio.wav")
```

By default, Pydub loads audio files as mono with a sample rate of 44100. We can convert the audio to stereo and change the sample rate if needed:

```python
audio = audio.set_channels(2)  # Convert to stereo
audio = audio.set_frame_rate(22050)  # Change sample rate to 22050 Hz
```

To generate the spectrogram, we need to convert the audio to a numerical representation. We can do this by converting it to a numpy array:

```python
samples = np.array(audio.get_array_of_samples())
```

Once we have the numerical representation, we can use the `plt.specgram` function from matplotlib to generate the spectrogram:

```python
plt.specgram(samples, NFFT=1024, Fs=audio.frame_rate, noverlap=512)
plt.xlabel('Time (s)')
plt.ylabel('Frequency (Hz)')
plt.colorbar(format='%+2.0f dB')
plt.show()
```

In the above code, `NFFT` specifies the length of each FFT segment, `Fs` is the sample rate, and `noverlap` controls the overlap between adjacent segments. The resulting spectrogram is displayed using `plt.show()`.

### Conclusion

In this tutorial, we learned how to generate audio spectrograms using the Pydub library in Python. Spectrograms provide valuable insights into the frequencies present in an audio signal, and can be helpful in various audio analysis tasks. Pydub simplifies the process of audio manipulation and makes it easy to generate and explore spectrograms.