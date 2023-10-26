---
layout: post
title: "[python] Time stretching audio with Pydub"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Have you ever wanted to slow down or speed up an audio file without affecting its pitch? This process is known as time stretching, and it can be achieved using the Pydub library in Python. In this blog post, we will explore how to use Pydub to perform time stretching on audio files.

## Introduction to Pydub

Pydub is a simple and easy-to-use audio processing library in Python. It provides a high-level interface for manipulating audio files. Pydub supports various file formats, such as WAV, MP3, and more.

To install Pydub, you can use pip:

```python
pip install pydub
```

## Time Stretching with Pydub

To time stretch an audio file using Pydub, we need to follow these steps:

1. Import the necessary modules:
```python
from pydub import AudioSegment
```
2. Load the audio file:
```python
audio = AudioSegment.from_file("input.wav")
```
3. Time stretch the audio using the `speedup` or `slowdown` method:
```python
streched_audio = audio.speedup(playback_speed=1.5)  # Increase the playback speed
# OR
streched_audio = audio.slowdown(playback_speed=0.8)  # Decrease the playback speed
```
4. Export the time-stretched audio to a new file:
```python
streched_audio.export("output.wav", format="wav")
```

Make sure to replace `"input.wav"` with the path of your audio file. The `speedup` and `slowdown` methods take a `playback_speed` parameter that determines how much to speed up or slow down the audio. A value less than 1 slows down the audio, while a value greater than 1 speeds it up.

## Example

Here's an example that time stretches an audio file:

```python
from pydub import AudioSegment

audio = AudioSegment.from_file("input.wav")
streched_audio = audio.slowdown(playback_speed=0.8)
streched_audio.export("output.wav", format="wav")
```

In this example, an audio file named `"input.wav"` is loaded, and its playback speed is decreased by 20% using the `slowdown` method. The time-stretched audio is then exported to a new file named `"output.wav"`.

## Conclusion

Time stretching audio can be a useful technique in various applications, such as audio production, music remixing, and sound design. Pydub provides a convenient way to perform time stretching on audio files in Python, allowing you to easily manipulate the playback speed without altering the pitch.

Give it a try and experiment with different playback speeds to achieve the desired time stretching effect. Happy coding!

## References

- [Pydub documentation](https://github.com/jiaaro/pydub)
- [Pydub on PyPI](https://pypi.org/project/pydub/)