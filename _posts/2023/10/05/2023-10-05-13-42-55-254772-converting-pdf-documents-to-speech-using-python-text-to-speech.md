---
layout: post
title: "[python] Converting PDF documents to speech using Python text-to-speech"
description: " "
date: 2023-10-05
tags: [python]
comments: true
share: true
---

In this tutorial, we will explore how to convert PDF documents into speech using Python's text-to-speech library. With this functionality, you can have your computer read out the content of a PDF document, making it accessible to individuals with visual impairments or simply providing a convenient way to listen to documents hands-free.

## Table of Contents
- [Installing the Required Libraries](#installing-the-required-libraries)
- [Converting PDF to Text](#converting-pdf-to-text)
- [Converting Text to Speech](#converting-text-to-speech)
- [Putting It All Together](#putting-it-all-together)
- [Conclusion](#conclusion)

## Installing the Required Libraries

To get started, we need to install two Python libraries - `PyPDF2` for extracting text from PDF files and `gTTS` (Google Text-to-Speech) for converting text to speech. Open your terminal or command prompt and run the following commands:

```python
pip install PyPDF2
pip install gTTS
```

## Converting PDF to Text

Once the libraries are installed, we can proceed with extracting text from PDF files. First, we need to import the necessary libraries:

```python
import PyPDF2
```

Next, we can define a function that accepts the path to a PDF file and returns its extracted text:

```python
def extract_text_from_pdf(file_path):
    with open(file_path, 'rb') as file:
        pdf = PyPDF2.PdfFileReader(file)
        text = ''
        for page_num in range(pdf.numPages):
            page = pdf.getPage(page_num)
            text += page.extractText()
    return text
```

The `extract_text_from_pdf` function opens the PDF file in binary mode, creates a `PdfFileReader` object, and iterates over each page to extract its text using the `extractText` method of the `page` object. The extracted text is then concatenated and returned.

## Converting Text to Speech

To convert text to speech, we will utilize the `gTTS` library. First, import the necessary module:

```python
from gtts import gTTS
```

Next, we can define a function that accepts text and saves it as an audio file:

```python
def convert_text_to_speech(text, output_file):
    tts = gTTS(text)
    tts.save(output_file)
```

The `convert_text_to_speech` function creates a `gTTS` object with the provided text and saves it as an audio file specified by the `output_file` parameter.

## Putting It All Together

Now that we have the functions to extract text from a PDF and convert it to speech, let's put everything together in a script:

```python
import PyPDF2
from gtts import gTTS

def extract_text_from_pdf(file_path):
    with open(file_path, 'rb') as file:
        pdf = PyPDF2.PdfFileReader(file)
        text = ''
        for page_num in range(pdf.numPages):
            page = pdf.getPage(page_num)
            text += page.extractText()
    return text

def convert_text_to_speech(text, output_file):
    tts = gTTS(text)
    tts.save(output_file)

# Example usage
pdf_file = 'sample.pdf'
output_audio = 'sample.mp3'

extracted_text = extract_text_from_pdf(pdf_file)
convert_text_to_speech(extracted_text, output_audio)
```

Make sure to replace `sample.pdf` with the path to your PDF document and `sample.mp3` with the desired output audio file name. 

## Conclusion

In this tutorial, we explored how to convert PDF documents into speech using Python's text-to-speech library. By extracting text from PDF files and converting it to audio, we can make documents more accessible and provide a convenient way to listen to text. Feel free to customize and enhance the code according to your specific requirements.