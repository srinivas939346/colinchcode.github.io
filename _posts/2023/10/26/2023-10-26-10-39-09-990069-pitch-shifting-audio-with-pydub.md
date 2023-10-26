---
layout: post
title: "[python] Pitch shifting audio with Pydub"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In this tutorial, we will explore how to pitch shift audio using Pydub, a simple and easy-to-use audio processing library for Python. Pitch shifting alters the frequency of audio signals, effectively changing the pitch without affecting the playback speed.

## Prerequisites

Before we get started, make sure you have the following prerequisites installed:

- Python (version 3.6 or later)
- Pydub library (`pip install pydub`)

## Getting Started

First, let's import the necessary modules:

```python
from pydub import AudioSegment
from pydub.playback import play
```

Next, we'll load an audio file using `AudioSegment.from_file()` method:

```python
audio = AudioSegment.from_file('original_audio.wav', format='wav')
```

Now, let's define the desired pitch shift value. A positive value will increase the pitch, while a negative value will decrease it:

```python
pitch_shift = 5  # Increasing the pitch by 5 semitones
```

## Pitch Shifting

To pitch shift the audio, we can use the `pydub.effects.pitch_shift()` method. This method takes the input audio, the pitch shift value, and returns a new AudioSegment object with the modified pitch:

```python
shifted_audio = audio.pydub.effects.pitch_shift(audio, pitch_shift)
```

## Playback

To listen to the pitch-shifted audio, we can use the `play()` function from the `pydub.playback` module:

```python
play(shifted_audio)
```

## Exporting

If you want to save the pitch-shifted audio to a file, you can use the `export()` method of the AudioSegment object:

```python
shifted_audio.export('shifted_audio.wav', format='wav')
```

## Complete Example

Here's a complete example that combines all the steps:

```python
from pydub import AudioSegment
from pydub.playback import play

audio = AudioSegment.from_file('original_audio.wav', format='wav')
pitch_shift = 5

shifted_audio = audio.pydub.effects.pitch_shift(audio, pitch_shift)
play(shifted_audio)
shifted_audio.export('shifted_audio.wav', format='wav')
```

## Conclusion

In this tutorial, we learned how to use Pydub to pitch shift audio. With Pydub's easy-to-use methods, you can quickly alter the pitch of audio files and experiment with different sounds.