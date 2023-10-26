---
layout: post
title: "[python] Pitch detection and manipulation with Pydub"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

## Introduction

Pitch detection and manipulation are common tasks in audio processing. Whether you want to analyze the pitch of a recorded voice, tune a musical instrument, or change the pitch of a song, having the ability to work with pitch is essential.

In this blog post, we will explore how to detect and manipulate pitches using Pydub, a powerful audio processing library for Python. Pydub provides a simple and intuitive interface to work with audio files, making it a great choice for pitch-related tasks.

## Prerequisites

Before we get started, make sure you have Pydub installed. You can install it using pip:

```shell
pip install pydub
```

Also, make sure you have some audio files available for testing.

## Pitch Detection

Pitch detection is the process of estimating the fundamental frequency of a sound. One common approach is to use the Autocorrelation method, which involves finding the lag at which the autocorrelation of a signal is at its maximum.

Let's see how we can perform pitch detection using Pydub:

```python
from pydub import AudioSegment
from pydub.playback import play

def detect_pitch(file_path):
    audio = AudioSegment.from_file(file_path)
    samples = audio.get_array_of_samples()
    length = len(samples)
    
    # Perform autocorrelation
    autocorrelation = []
    for lag in range(length):
        correlation = sum(samples[i] * samples[i + lag] for i in range(length - lag))
        autocorrelation.append(correlation)
    
    # Find highest correlation
    max_correlation = max(autocorrelation)
    max_index = autocorrelation.index(max_correlation)
    
    # Calculate pitch frequency
    sample_rate = audio.frame_rate
    pitch = sample_rate / max_index
    
    return pitch

# Example usage
file_path = "test_audio.wav"
pitch = detect_pitch(file_path)
print(f"Detected pitch: {pitch} Hz")
```

In this code, we first load the audio file using `AudioSegment.from_file()`. We then retrieve the raw audio samples using `get_array_of_samples()`. Next, we perform autocorrelation on the samples to find the lag with the highest correlation. Finally, we calculate the pitch frequency using the sample rate and the lag.

## Pitch Manipulation

Now that we know how to detect pitch, let's move on to pitch manipulation. Pydub provides a handy method `rate_change()` that allows us to change the pitch of an audio file.

Here's an example of how to change the pitch of an audio file using Pydub:

```python
from pydub import AudioSegment
from pydub.playback import play

def change_pitch(file_path, semitones):
    audio = AudioSegment.from_file(file_path)
    
    # Calculate speed multiplier based on semitones
    speed_multiplier = 2 ** (semitones / 12)
    
    # Change pitch by altering playback speed
    pitched_audio = audio._spawn(audio.raw_data, overrides={
        "frame_rate": int(audio.frame_rate * speed_multiplier)
    })
    
    # Apply effects and export
    adjusted_audio = pitched_audio.set_frame_rate(audio.frame_rate)
    adjusted_audio.export("pitch_adjusted_audio.wav", format="wav")
    
    # Play adjusted audio
    play(adjusted_audio)

# Example usage
file_path = "original_audio.wav"
semitones = 2
change_pitch(file_path, semitones)
```

In this code, we first load the audio file using `AudioSegment.from_file()`. We then calculate the speed multiplier based on the desired pitch change in semitones. Next, we use the `_spawn()` method to change the frame rate of the audio with the calculated multiplier. We apply any other desired effects and then export the adjusted audio to a new file.

## Conclusion

In this blog post, we explored how to detect and manipulate pitches using Pydub. We learned how to perform pitch detection using the Autocorrelation method and how to change the pitch of an audio file using the `rate_change()` function provided by Pydub. 

Pitch detection and manipulation are powerful techniques in audio processing, and Pydub makes it easy and convenient to work with pitches in Python.

Give it a try and start exploring the possibilities of pitch detection and manipulation in your audio projects!