---
layout: post
title: "[python] MicroPython and audio processing"
description: " "
date: 2023-10-31
tags: [python]
comments: true
share: true
---

MicroPython is a subset of the Python programming language that is optimized to run on resource-constrained microcontrollers. While it may not have all the features of a full-fledged Python, it still provides a great platform for building projects that require embedded systems.

One interesting use case of MicroPython is audio processing. With the help of a few external components, it is possible to capture, manipulate, and playback audio on a microcontroller running MicroPython.

## Hardware Requirements

To work with audio in MicroPython, you will need the following components:

1. Microcontroller board: Such as an ESP32 or an Arduino board.
2. Audio codec: An external codec like the PCM5102A, which provides analog-to-digital and digital-to-analog conversion capabilities.
3. Speaker or headphone: To listen to the output sound.

## Wiring

The audio codec needs to be connected to the microcontroller board using the appropriate pins. Refer to the datasheet of the codec for the pinout details. In most cases, you will need to connect the I2S data, clock, and LRCLK pins.

## MicroPython Libraries

There are several MicroPython libraries available for audio processing. One popular library is the `audioio` module, which provides functions to capture and play audio samples.

To use the `audioio` module, you need to install it on your microcontroller. The library can be installed via `upip`, the package manager for MicroPython.

```python
import upip

upip.install("micropython-audio")
```

## Capturing Audio

To capture audio with MicroPython, you need to configure the codec and initialize the `audioio` module. Here is an example code snippet that shows how to capture audio for a specified duration:

```python
import audioio
import audiobusio

sample_length = 2  # Duration in seconds
sample_rate = 48000
sample_width = 16

# Configure and initialize audio input
record_input = audiobusio.I2S(samplerate=sample_rate, samplewidth=sample_width, channel_count=1)
audio_input = audioio.AudioIn(board.SDA, board.SCL, bit_depth=sample_width)

# Create an audio buffer
sample_buffer = audioio.RawSample(width=sample_width, channels=1, sample_rate=sample_rate)

# Capture audio
audio_input.start(sample_buffer)
time.sleep(sample_length)
audio_input.stop()

# Process captured audio data
for sample in sample_buffer:
    # Process the audio data here
    pass
```

## Playing Audio

To play audio with MicroPython, you can use the same `audioio` module. Here is an example code snippet that shows how to play a pre-recorded audio file:

```python
import audioio

# Open the audio file
audio_file = open("audio.wav", "rb")

# Initialize the audio output
audio_output = audioio.AudioOut(board.SDA, board.SCL)

# Play the audio
audio_output.play(audio_file)

# Wait until the audio finishes playing
while audio_output.playing:
    pass

# Close the file
audio_file.close()
```

## Conclusion

MicroPython provides a lightweight yet powerful platform for audio processing on microcontrollers. By combining it with the appropriate hardware and libraries, you can build projects that involve audio capturing, manipulation, and playback. So if you're interested in working with audio in an embedded context, give MicroPython a try!

---

References:
- [MicroPython Documentation](https://docs.micropython.org/en/latest/)
- [MicroPython Audio](https://github.com/micropython/micropython-lib/tree/master/audio)