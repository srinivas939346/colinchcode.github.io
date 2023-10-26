---
layout: post
title: "[python] Exporting audio files with Pydub"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Pydub is a powerful audio processing library in Python that allows you to manipulate audio files in various formats. One common use case is exporting audio files in different formats, such as converting a WAV file to MP3 or vice versa. In this blog post, we'll explore how to export audio files using Pydub.

## Table of Contents
- [Installing Pydub](#installing-pydub)
- [Exporting audio files](#exporting-audio-files)
  - [Export as WAV](#export-as-wav)
  - [Export as MP3](#export-as-mp3)
- [Conclusion](#conclusion)

## Installing Pydub

To begin, you need to have Pydub installed on your machine. You can install it using pip by running the following command:

```bash
pip install pydub
```

Once installed, you can import it in your Python script:

```python
from pydub import AudioSegment
```

## Exporting audio files

Pydub supports a wide range of audio formats, including WAV, MP3, FLAC, and more. Let's explore how to export audio files in different formats.

### Export as WAV

To export an audio file as WAV, you can use the `export` method of `AudioSegment`. Here's an example:

```python
audio = AudioSegment.from_mp3("input.mp3")
audio.export("output.wav", format="wav")
```

In the above code, we first load the input MP3 file using `AudioSegment.from_mp3`. Then, we export it as a WAV file using the `export` method, specifying the output file name and format.

### Export as MP3

Similarly, you can export audio files as MP3 using Pydub. Here's an example:

```python
audio = AudioSegment.from_wav("input.wav")
audio.export("output.mp3", format="mp3")
```

In the above code, we load the input WAV file using `AudioSegment.from_wav` and export it as an MP3 file using the `export` method.

## Conclusion

Exporting audio files in different formats is a common requirement in audio processing applications. Pydub provides a simple and efficient way to export audio files to various formats, such as WAV or MP3. With its easy-to-use interface, you can quickly convert audio files using just a few lines of code. Give it a try in your next audio project!

**References**
- [Pydub documentation](https://github.com/jiaaro/pydub)