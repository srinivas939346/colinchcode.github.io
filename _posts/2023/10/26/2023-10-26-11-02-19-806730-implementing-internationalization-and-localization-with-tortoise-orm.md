---
layout: post
title: "[python] Implementing internationalization and localization with Tortoise ORM"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

When building applications that cater to a global audience, it's crucial to provide support for internationalization and localization. This ensures that users from different countries can use your application in their preferred language. In this blog post, we will explore how to implement internationalization and localization with Tortoise ORM, a Python ORM for asyncio.

## Table of Contents
- [What is internationalization and localization?](#what-is-internationalization-and-localization)
- [Setting up Tortoise ORM for internationalization](#setting-up-tortoise-orm-for-internationalization)
- [Creating translation files](#creating-translation-files)
- [Using translations in your application](#using-translations-in-your-application)
- [Conclusion](#conclusion)

## What is internationalization and localization?

**Internationalization (i18n)** is the process of designing and developing an application in a way that makes it easy to adapt to different languages, regions, and cultures without any code changes. It involves separating UI text, formatting, and other localized content from the source code.

**Localization (l10n)**, on the other hand, refers to adapting an application to a specific language, region, or culture. It involves translating UI text, formatting dates and numbers based on locale-specific rules, and addressing other cultural nuances.

## Setting up Tortoise ORM for internationalization

To get started with internationalization and localization in Tortoise ORM, we need to set up the necessary configurations. First, make sure you have Tortoise ORM installed:

```
pip install tortoise-orm
```

Next, define the available languages in your application by setting the `TORTOISE_ORM_I18N_AVAILABLE_LANGUAGES` environment variable in your settings:

```python
import os

os.environ["TORTOISE_ORM_I18N_AVAILABLE_LANGUAGES"] = "en,fr,es"
```

Make sure to replace `"en,fr,es"` with the languages you want to support in your application.

## Creating translation files

To enable translation of your application's text, you'll need to create translation files for each supported language. These files will contain key-value pairs, where the keys represent the original text in your application and the values represent the translated text.

The translation files should be placed in a directory called `locales` at the root of your project. Each translation file should be named with the respective language code, followed by `.json`. For example, `en.json`, `fr.json`, `es.json`.

Here's an example of a translation file (`en.json`):

```json
{
  "Hello": "Hello",
  "Welcome": "Welcome",
  "Save": "Save",
  "Cancel": "Cancel"
}
```

## Using translations in your application

Now that we have set up the necessary configurations and created translation files, we can start using the translations in our application.

First, import the necessary modules:

```python
from tortoise import fields, models
from tortoise.contrib import i18n
```

Next, define a `TranslationModel` that will be used to retrieve translated text:

```python
class Translation(models.Model):
    key = fields.CharField(max_length=255, unique=True)
    translations = i18n.TranslatedField()
```

To retrieve translated text, use the `get_translation` method:

```python
async def get_translated_text(key: str, language: str) -> str:
    translation = await Translation.filter(key=key).first().prefetch_related('translations')
    return translation.translations.get(language, '')
```

To use the translated text in your application, simply call the `get_translated_text` function with the desired key and language:

```python
translated_text = await get_translated_text('Hello', 'fr')
print(translated_text)  # Output: Bonjour
```

## Conclusion

In this blog post, we explored how to implement internationalization and localization with Tortoise ORM. By following the steps outlined, you can make your application ready to support multiple languages and cater to a global audience.