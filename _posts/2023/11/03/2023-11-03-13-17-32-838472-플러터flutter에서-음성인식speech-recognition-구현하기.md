---
layout: post
title: "[flutter] 플러터(Flutter)에서 음성인식(Speech Recognition) 구현하기"
description: " "
date: 2023-11-03
tags: [flutter]
comments: true
share: true
---

플러터(Flutter)는 Google에서 개발한 크로스 플랫폼 앱 개발 프레임워크로, iOS와 Android 앱을 동시에 개발할 수 있습니다. 이 글에서는 플러터를 사용하여 음성인식 기능을 구현하는 방법에 대해 알아보겠습니다.

## 음성인식 라이브러리

플러터에서 음성인식 기능을 구현하기 위해서는 음성인식 라이브러리를 사용해야 합니다. 그 중에서도 `speech_recognition` 라이브러리가 가장 널리 사용되고 있습니다.

`speech_recognition` 라이브러리를 사용하기 위해서는 프로젝트의 `pubspec.yaml` 파일에 다음과 같이 의존성을 추가해야 합니다:

```yaml
dependencies:
  speech_recognition: ^2.0.0
```

의존성을 추가한 후에는 `pub get` 명령어를 실행하여 의존성을 설치해야 합니다.

## 음성인식 구현하기

음성인식 기능을 구현하기 위해 다음의 단계를 따를 수 있습니다:

1. 음성인식 객체 생성하기: 음성인식을 위한 객체를 생성합니다.

```dart
SpeechRecognition _speechRecognition = SpeechRecognition();
```

2. 사용 가능한 언어 설정하기: 음성인식을 위해 사용 가능한 언어를 설정합니다.

```dart
_speechRecognition.setAvailabilityHandler((bool result) {
  setState(() => _isAvailable = result);
});

// 사용 가능한 언어 목록 조회
List<LocaleName> _localeNames = [];
_speechRecognition.setRecognitionStartedHandler(() {
  setState(() => _isListening = true);
});
_speechRecognition.setRecognitionResultHandler((String speech) {
  setState(() => _speech = speech);
});
_speechRecognition.setRecognitionCompleteHandler(() {
  setState(() {
    _isListening = false;
    _speechController.text = _speech;
  });
});

await _speechRecognition.activate();
_localeNames = await _speechRecognition.locales();
```

3. 음성인식 시작하기: 음성인식을 시작합니다.

```dart
_speechRecognition.listen(locale: selectedLang);
```

4. 음성인식 중지하기: 음성인식을 중지합니다.

```dart
_speechRecognition.stop();
```

이제 플러터에서 음성인식 기능을 구현하는 방법을 알아보았습니다. 이를 활용하여 다양한 음성인식 애플리케이션을 개발할 수 있습니다. 

더 자세한 내용은 [이 곳](https://pub.dev/packages/speech_recognition)에서 확인할 수 있습니다.

## 참고 자료

- [플러터(Flutter) 공식 사이트](https://flutter.dev/)
- [speech_recognition 라이브러리](https://pub.dev/packages/speech_recognition)