---
layout: post
title: "[python] Applying audio filters with Pydub"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Pydub is a powerful Python library that allows you to work with audio files in a simple and efficient manner. One of the many things you can do with Pydub is applying audio filters to your audio files. In this article, we will explore some common audio filters and see how they can be applied using Pydub.

## Table of Contents
- [Installing Pydub](#installing-pydub)
- [Applying Filters](#applying-filters)
  - [Low Pass Filter](#low-pass-filter)
  - [High Pass Filter](#high-pass-filter)
  - [Equalizer](#equalizer)
- [Conclusion](#conclusion)

## Installing Pydub
Before we start, make sure you have Pydub installed. You can install it using pip:

```shell
pip install pydub
```

## Applying Filters
Once you have Pydub installed, you can start applying audio filters to your audio files.

### Low Pass Filter
A low pass filter allows only frequencies below a certain cutoff frequency to pass through. To apply a low pass filter using Pydub, you can use the `low_pass_filter` method:

```python
from pydub import AudioSegment

audio = AudioSegment.from_file("input.wav")

filtered_audio = audio.low_pass_filter(1000)  # Cutoff frequency: 1000Hz

filtered_audio.export("output.wav", format="wav")
```

### High Pass Filter
A high pass filter allows only frequencies above a certain cutoff frequency to pass through. To apply a high pass filter using Pydub, you can use the `high_pass_filter` method:

```python
from pydub import AudioSegment

audio = AudioSegment.from_file("input.wav")

filtered_audio = audio.high_pass_filter(1000)  # Cutoff frequency: 1000Hz

filtered_audio.export("output.wav", format="wav")
```

### Equalizer
An equalizer allows you to boost or attenuate specific frequency bands in your audio. To apply an equalizer filter using Pydub, you can use the `apply_gain_stereo` method:

```python
from pydub import AudioSegment

audio = AudioSegment.from_file("input.wav")

equalized_audio = audio.apply_gain_stereo(2, 1000)  # Boosting 2dB at 1000Hz

equalized_audio.export("output.wav", format="wav")
```

You can customize the equalizer by specifying different gain values at different frequencies.

## Conclusion
Pydub makes it easy to apply audio filters to your audio files. Whether you want to apply a low pass filter, a high pass filter, or an equalizer, Pydub provides simple methods to achieve these tasks. Give it a try and experiment with different filters to shape the sound of your audio files. Happy filtering!