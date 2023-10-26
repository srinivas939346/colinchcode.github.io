---
layout: post
title: "[python] Frequency domain analysis with Pydub"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In this tutorial, we will explore how to perform frequency domain analysis on audio signals using the Pydub library in Python. Pydub is a simple and easy-to-use library for audio processing.

## Table of Contents
1. [Introduction](#introduction)
2. [Installing Pydub](#installing-pydub)
3. [Loading and Playing Audio](#loading-and-playing-audio)
4. [Performing Frequency Domain Analysis](#performing-frequency-domain-analysis)
5. [Visualizing the Spectrogram](#visualizing-the-spectrogram)

## Introduction<a name="introduction"></a>

Frequency domain analysis involves analyzing the frequency content of an audio signal. It helps in understanding various aspects of the audio, such as identifying the dominant frequencies or detecting specific patterns.

Pydub makes it easy to perform frequency domain analysis by providing tools to convert audio into the frequency domain representation using the Fast Fourier Transform (FFT).

## Installing Pydub<a name="installing-pydub"></a>

Before we begin, let's make sure Pydub is installed. You can install it using pip by running the following command:

```bash
pip install pydub
```

## Loading and Playing Audio<a name="loading-and-playing-audio"></a>

To get started, we need an audio file to work with. Pydub supports various audio formats, including WAV, MP3, and FLAC. You can use any audio file of your choice.

Let's start by loading an audio file and playing it using Pydub:

```python
from pydub import AudioSegment
from pydub.playback import play

# Load audio file
audio = AudioSegment.from_file("sample_audio.wav")

# Play audio
play(audio)
```

Make sure to replace `"sample_audio.wav"` with the path to your audio file.

## Performing Frequency Domain Analysis<a name="performing-frequency-domain-analysis"></a>

Pydub provides a `fft` method that allows us to convert an audio signal into the frequency domain representation. Here's how you can use it:

```python
from pydub import AudioSegment

# Convert audio to frequency domain
freq_domain = audio.fft()
```

The `freq_domain` variable will contain the frequency domain representation of the audio signal.

## Visualizing the Spectrogram<a name="visualizing-the-spectrogram"></a>

To visualize the frequency content of the audio signal, we can create a spectrogram using `matplotlib`. A spectrogram is a 2D representation that displays how the frequencies in an audio signal vary with time.

Here's an example of how you can visualize the spectrogram of the audio signal:

```python
import matplotlib.pyplot as plt

# Create spectrogram
plt.specgram(audio.get_array_of_samples(), Fs=audio.frame_rate)

# Set labels and title
plt.xlabel('Time')
plt.ylabel('Frequency')
plt.title('Spectrogram')

# Display the spectrogram
plt.show()
```

The `plt.specgram` function takes the audio samples and the sample rate (`audio.get_array_of_samples()` and `audio.frame_rate`), and plots the spectrogram.

That's it! You can now perform frequency domain analysis on audio signals using Pydub in Python. Experiment with different audio files and explore the frequency content of your audio.