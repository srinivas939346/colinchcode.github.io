---
layout: post
title: "[python] Modifying audio pitch and tempo with Pydub"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In this post, we will explore how to modify audio pitch and tempo using the Pydub library in Python. Pydub is a simple and easy-to-use library for audio processing tasks, including manipulating audio files.

## Table of Contents
- [Introduction](#introduction)
- [Modifying Pitch](#modifying-pitch)
- [Modifying Tempo](#modifying-tempo)
- [Conclusion](#conclusion)

## Introduction

Pydub provides a straightforward way to load, manipulate, and export audio files. Before we begin, make sure to install Pydub by running the following command:

```bash
pip install pydub
```

Once Pydub is installed, we can proceed with modifying the pitch and tempo of audio files.

## Modifying Pitch

Changing the pitch of an audio file refers to altering its perceived frequency. By increasing or decreasing the pitch, we can make the audio sound higher or lower. Pydub allows us to manipulate pitch using the `pydub.effects.pitch_shift` method.

Here's an example that demonstrates how to increase the pitch of an audio file by 3 semitones:

```python
from pydub import AudioSegment
from pydub.effects import pitch_shift

audio = AudioSegment.from_file("input.wav")
shifted_audio = pitch_shift(audio, 3)

shifted_audio.export("output.wav", format="wav")
```

In the above code snippet, we first load the audio file `input.wav` using `AudioSegment`. Then, we use the `pitch_shift` function to shift the pitch of the audio by 3 semitones. Finally, we export the modified audio to the file `output.wav`.

## Modifying Tempo

Altering the tempo of an audio file refers to changing its playback speed while maintaining the same pitch. Pydub allows us to adjust the tempo of audio using the `pydub.effects.time_stretch` method.

Let's see how to double the tempo of an audio file:

```python
from pydub import AudioSegment
from pydub.effects import time_stretch

audio = AudioSegment.from_file("input.wav")
stretched_audio = time_stretch(audio, 2.0)

stretched_audio.export("output.wav", format="wav")
```

In the code above, we load the audio file `input.wav` and then apply the `time_stretch` function with a multiplier of 2.0 to double the tempo. Finally, we export the modified audio to `output.wav`.

## Conclusion

In this post, we've learned how to modify audio pitch and tempo using Pydub. We've seen examples of increasing the pitch of an audio file and doubling its tempo. Pydub is a powerful library for audio processing tasks and provides various functions to manipulate audio files easily. Explore the Pydub documentation for more advanced features and techniques.

References:
- [Pydub Documentation](https://github.com/jiaaro/pydub)