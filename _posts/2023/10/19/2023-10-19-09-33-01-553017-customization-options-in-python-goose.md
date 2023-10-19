---
layout: post
title: "[python] Customization options in Python Goose"
description: " "
date: 2023-10-19
tags: [python]
comments: true
share: true
---

Python Goose is a web article extraction library that allows you to extract and clean the main content from web pages. In addition to its default settings for article extraction, Python Goose provides several customization options that can be used to fine-tune the extraction process.

## 1. Parser options

Python Goose provides different parser options to handle various types of webpages. By default, it uses BeautifulSoup as the HTML parser. However, you can choose a different parser that suits your needs. For example, you can use 'lxml' or 'html5lib' instead of BeautifulSoup.

To specify a parser option, you can pass it as a parameter when creating an instance of the Goose object:

```
from goose3 import Goose

g = Goose(parser='lxml')
```

## 2. Configuration options

Python Goose allows you to customize its behavior through configuration options. These options can be set when creating an instance of the Goose object or by modifying the default configuration file.

Some of the common configuration options include:

- `use_meta_language`: Set to `True` if you want to extract the language of the article from the HTML meta tag.
- `enable_image_fetching`: Set to `True` if you want to download and save images found in the article.
- `target_language`: Specify the target language for article extraction.
- `browser_user_agent`: Customize the user agent string to be used when fetching webpages.

To set a configuration option, you can use the `config` parameter when creating the Goose object:

```
from goose3 import Goose

config = {
    'use_meta_language': True,
    'enable_image_fetching': True,
    'target_language': 'en',
    'browser_user_agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3'
}

g = Goose(config=config)
```

## 3. Advanced options

Python Goose provides a set of advanced options that allow you to customize the behavior of the article extraction process in more detail.

Some of the advanced options include:

- `min_words`: Set the minimum number of words a paragraph should have to be considered as an article.
- `max_target_lengh`: Specify the maximum length (in characters) of the extracted article.
- `use_anchors`: Set to `True` if you want to extract text from HTML anchors.
- `target_max_article_sentences`: Set the maximum number of sentences to consider for article extraction.

To set an advanced option, you can use the `options` parameter when calling the `extract` method of the Goose object:

```python
from goose3 import Goose

g = Goose()
article = g.extract(url='https://example.com', options={'min_words': 300, 'max_target_length': 5000})
```

These are just a few examples of the customization options available in Python Goose. For a complete list of options and their descriptions, refer to the official documentation of Python Goose.

## Conclusion

Python Goose provides various customization options that allow you to tailor the web article extraction process to your specific requirements. By choosing the right parser, configuring the library, and using advanced options, you can achieve more accurate and efficient article extraction from web pages.