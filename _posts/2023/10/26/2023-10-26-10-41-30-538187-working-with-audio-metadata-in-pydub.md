---
layout: post
title: "[python] Working with audio metadata in Pydub"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

As a Python developer working on audio processing, you often come across situations where you need to extract or modify metadata from audio files. Pydub, a powerful audio processing library, provides a simple and intuitive way to handle audio metadata.

In this blog post, we will explore how to work with audio metadata using Pydub. We will cover the following topics:

1. Introduction to Pydub
2. Retrieving Metadata from Audio Files
3. Modifying Metadata in Audio Files
4. Saving Changes to Audio Files

Let's get started!

## Introduction to Pydub

Pydub is a high-level audio processing library built on top of ffmpeg and provides a simple API for manipulating audio files. It is widely used and known for its ease of use and powerful features.

To get started, you need to install Pydub by running the following command:

```shell
pip install pydub
```

Once installed, you can import Pydub in your Python script as follows:

```python
from pydub import AudioSegment
```

Now that we have Pydub set up, let's move on to retrieving metadata from audio files.

## Retrieving Metadata from Audio Files

Pydub makes it easy to extract metadata from audio files. You can use the `AudioSegment` class to load an audio file, and then access its metadata using the `metadata` attribute.

```python
audio = AudioSegment.from_file("example.mp3")

# Retrieving metadata
metadata = audio.metadata
title = audio.metadata['title']
artist = audio.metadata['artist']
duration = audio.duration_seconds

print(f"Title: {title}")
print(f"Artist: {artist}")
print(f"Duration: {duration}s")
```

In the above example, we load an audio file named "example.mp3" and retrieve its metadata. We extract the title, artist, and duration of the audio file and display them using the `print` function.

## Modifying Metadata in Audio Files

Pydub also provides functionality to modify metadata in audio files. You can simply update the `metadata` attribute of an `AudioSegment` object and save the changes back to the audio file using the `export` method.

```python
audio = AudioSegment.from_file("example.mp3")

# Modifying metadata
audio.metadata['title'] = "New Title"
audio.export("modified_example.mp3", format="mp3")
```

In the above code snippet, we load an audio file called "example.mp3" and update its title. We then export the modified audio to a new file named "modified_example.mp3" using the `export` method.

## Saving Changes to Audio Files

After modifying metadata or making any other changes to the audio, you need to save the changes to the audio file. Pydub provides the `export` method to save the modified audio to a file.

```python
audio.export("modified_example.mp3", format="mp3")
```

In the above example, we export the modified audio to a new file named "modified_example.mp3". The `format` parameter specifies the desired audio format, in this case, "mp3".

You can also specify other audio formats, such as "wav", "flac", or "ogg", based on your requirements.

## Conclusion

In this blog post, we explored how to work with audio metadata using Pydub. We covered retrieving metadata, modifying metadata, and saving changes to audio files. Pydub provides a convenient and easy-to-use API for handling audio metadata, making your audio processing tasks much simpler.

To learn more about Pydub and its capabilities, refer to the official Pydub documentation [here](https://github.com/jiaaro/pydub).

Happy coding!