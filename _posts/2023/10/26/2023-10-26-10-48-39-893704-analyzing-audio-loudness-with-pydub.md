---
layout: post
title: "[python] Analyzing audio loudness with Pydub"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

In this blog post, we will explore how to analyze audio loudness using the Pydub library in Python. Pydub is a simple and easy-to-use library for audio processing tasks, including analyzing and manipulating audio files.

## Table of Contents
1. [Introduction](#introduction)
2. [Installing Pydub](#installing-pydub)
3. [Analyzing Audio Loudness](#analyzing-audio-loudness)
4. [Code Example](#code-example)
5. [Conclusion](#conclusion)

<a name="introduction"></a>
## Introduction

Audio loudness is a measure of the volume or intensity of sound. It is an important aspect of audio analysis and is often used in applications such as audio mastering, quality control, and audio normalization.

Pydub provides a convenient way to analyze audio loudness by implementing the ITU-R BS.1770-4 loudness standard. This standard measures loudness using a unit called "Loudness Units Full Scale" (LUFS). In simpler terms, LUFS quantifies the perceived loudness of an audio file.

<a name="installing-pydub"></a>
## Installing Pydub

First, let's install Pydub using pip:

```bash
pip install pydub
```

Once installed, we can import Pydub in our Python script and start analyzing audio loudness.

<a name="analyzing-audio-loudness"></a>
## Analyzing Audio Loudness

To analyze audio loudness with Pydub, we need an audio file. Pydub supports various audio formats like MP3, WAV, FLAC, etc. Once we have an audio file, we can load it using Pydub's `AudioSegment` class.

Once loaded, we can use the `dBFS` property of the `AudioSegment` class to obtain the loudness in dBFS (decibels relative to full scale). Positive values indicate loudness above 0 dBFS, while negative values indicate loudness below 0 dBFS.

In addition to obtaining the overall loudness, we can also analyze the loudness of specific sections or intervals within the audio file.

<a name="code-example"></a>
## Code Example

Here's a simple example that demonstrates how to analyze audio loudness using Pydub:

```python
from pydub import AudioSegment

# Load audio file
audio = AudioSegment.from_file("path/to/audio_file.mp3")

# Get overall loudness in dBFS
loudness = audio.dBFS
print(f"Overall Loudness: {loudness} dBFS")

# Analyze loudness of a specific section (between 10 and 20 seconds)
section = audio[10000:20000]
section_loudness = section.dBFS
print(f"Loudness of section: {section_loudness} dBFS")
```

In this example, we load an audio file using `AudioSegment.from_file()`. We then obtain the overall loudness using the `dBFS` property of the `AudioSegment` instance. Finally, we extract a specific section of the audio file using slicing and analyze its loudness.

<a name="conclusion"></a>
## Conclusion

Analyzing audio loudness is essential in various audio processing tasks. Pydub provides a straightforward way to analyze audio loudness using the ITU-R BS.1770-4 standard. By following the steps outlined in this blog post, you can easily incorporate audio loudness analysis into your Python projects using Pydub.