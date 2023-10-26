---
layout: post
title: "[python] Modifying audio sample rate with Pydub"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When working with audio files, you may sometimes need to modify their sample rate. The sample rate determines the number of audio samples per second, and changing it can affect the speed and quality of the audio playback. In this tutorial, we will learn how to use Pydub, a Python library for audio processing, to modify the sample rate of an audio file.

## Table of Contents
- [Installing Pydub](#installing-pydub)
- [Loading an audio file](#loading-an-audio-file)
- [Modifying the sample rate](#modifying-the-sample-rate)
- [Exporting the modified audio](#exporting-the-modified-audio)
- [Conclusion](#conclusion)
- [References](#references)

## Installing Pydub
Before we can start working with Pydub, we need to install it. Open your terminal and run the following command to install Pydub using pip:

```bash
pip install pydub
```

## Loading an audio file
To load an audio file using Pydub, we need to import the `AudioSegment` class from the `pydub` module. Then, we can use the `AudioSegment.from_file()` method to load the audio file. Here's an example:

```python
from pydub import AudioSegment

# Load the audio file
audio = AudioSegment.from_file('path/to/audio/file.mp3')
```

## Modifying the sample rate
Once we have loaded the audio file, we can modify its sample rate using the `set_frame_rate()` method of the `AudioSegment` object. The `set_frame_rate()` method takes the desired sample rate as an argument. For example, to change the sample rate to 44100 Hz, use the following code:

```python
new_sample_rate = 44100
modified_audio = audio.set_frame_rate(new_sample_rate)
```

## Exporting the modified audio
After modifying the sample rate, we might want to export the modified audio to a new file. To do this, we can use the `export()` method of the `AudioSegment` object. The `export()` method takes two arguments: the file format (e.g., "mp3", "wav", "ogg") and the output file path. Here's an example:

```python
output_file = 'path/to/output/file.mp3'
modified_audio.export(output_file, format='mp3')
```

## Conclusion
In this tutorial, we learned how to use Pydub to modify the sample rate of an audio file. By using the `set_frame_rate()` method of the `AudioSegment` object, we can easily change the sample rate to achieve the desired audio playback speed and quality. We also saw how to export the modified audio to a new file using the `export()` method.

## References
- Pydub documentation: [https://github.com/jiaaro/pydub](https://github.com/jiaaro/pydub)