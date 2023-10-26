---
layout: post
title: "[python] Converting audio formats with Pydub"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

Pydub is a powerful Python library that allows us to work with audio files easily. One of the common tasks when working with audio is converting from one format to another. In this article, we will learn how to use Pydub to convert audio formats.

## Installation

To start using Pydub, we need to install it first. Open your terminal or command prompt and run the following command:

```
pip install pydub
```

Pydub relies on FFmpeg to handle audio files, so make sure you have FFmpeg installed on your system too.

## Converting audio formats

Once Pydub is installed, we can begin converting audio formats. Let's say we have an audio file in the WAV format and we want to convert it to MP3. Here's how we can do it with Pydub:

```python
from pydub import AudioSegment

# Load the audio file
audio = AudioSegment.from_wav('input.wav')

# Export to MP3
audio.export('output.mp3', format='mp3')
```

In the above code, we first import the `AudioSegment` class from the `pydub` module. Next, we use the `from_wav` method to load the input WAV file. Finally, we use the `export` method to convert and save the audio to the desired format, which is MP3 in this case.

Pydub supports a wide range of audio formats, such as WAV, MP3, FLAC, OGG, and more. You can specify the desired format by passing it as an argument to the `format` parameter of the `export` method.

## Converting multiple audio files

If you have multiple audio files that you want to convert, you can use a loop to process each file. Here's an example that demonstrates how to convert a list of WAV files to MP3:

```python
from pydub import AudioSegment
import os

# Path to the directory containing the WAV files
input_dir = 'path/to/wav/files'

# Path to the directory to save the MP3 files
output_dir = 'path/to/mp3/files'

# Get the list of all WAV files in the input directory
wav_files = [f for f in os.listdir(input_dir) if f.endswith('.wav')]

for wav_file in wav_files:
    # Load the audio file
    audio = AudioSegment.from_wav(os.path.join(input_dir, wav_file))

    # Extract the file name without extension
    file_name = os.path.splitext(wav_file)[0]

    # Export to MP3
    audio.export(os.path.join(output_dir, f'{file_name}.mp3'), format='mp3')
```

In the above code, we first define the input and output directories. Then, we retrieve a list of all WAV files in the input directory using a list comprehension. Next, we iterate over each WAV file, load it, extract the filename without extension, and export it as an MP3 file with the same name in the output directory.

## Conclusion

Converting audio formats using Pydub is straightforward and can be done with just a few lines of code. Whether you need to convert a single file or multiple files, Pydub provides a convenient and efficient way to work with audio formats in Python.

Remember to check the Pydub documentation for more advanced features and options.

Happy coding!