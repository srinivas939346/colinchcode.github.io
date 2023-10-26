---
layout: post
title: "[python] Playing audio files with Pydub"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In this tutorial, we will learn how to play audio files using Pydub, a simple and easy-to-use Python library for audio processing. Pydub provides an intuitive and high-level API for manipulating audio files, making it a great tool for playing, modifying, and extracting audio.

## Prerequisites

Before we start, make sure you have Pydub installed. If not, you can install it using pip:

```shell
pip install pydub
```

Also, make sure you have some audio files (.mp3, .wav, etc.) available on your system to use for playback.

## Playing an audio file

Now that we have Pydub installed and our audio files ready, let's start playing an audio file using Pydub. 

First, import the necessary modules:
```python
from pydub import AudioSegment
from pydub.playback import play
```

Next, load the audio file using the `AudioSegment.from_file()` method:
```python
audio = AudioSegment.from_file('path/to/audio.mp3', format='mp3')
```

Finally, use the `play()` function to start playing the audio file:
```python
play(audio)
```
The `play()` function will play the audio file until it finishes.

You can also specify a specific part of the audio to play by using the `play()` function with the `start` and `end` parameters. For example, to play the first 10 seconds of the audio file:
```python
play(audio[:10000])  # Play the first 10 seconds (in milliseconds)
```

## Adjusting audio playback speed

Pydub allows us to adjust the playback speed of audio files easily. To change the playback speed, we can use the `speedup()` or `slowdown()` methods of the `AudioSegment` object.

Here's an example that plays an audio file at double speed:
```python
fast_audio = audio.speedup(playback_speed=2.0)
play(fast_audio)
```

And here's an example that plays an audio file at half speed:
```python
slow_audio = audio.slowdown(playback_speed=0.5)
play(slow_audio)
```

## Conclusion

In this tutorial, we have learned how to play audio files using Pydub. We have seen how to load an audio file, play it, and adjust its playback speed. Pydub provides a simple and convenient way to manipulate audio files in Python, making it a great choice for audio processing tasks.

To learn more about Pydub and its capabilities, you can refer to the official documentation: [Pydub Documentation](https://github.com/jiaaro/pydub)