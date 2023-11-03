---
layout: post
title: "[flutter] 플러터(Flutter)에서 국제화(Internationalization) 구현하기"
description: " "
date: 2023-11-03
tags: [flutter]
comments: true
share: true
---

플러터(Flutter)는 다국어 지원 기능을 구현하기 위해 국제화(Internationalization)를 제공합니다. 국제화를 구현하면 앱의 사용자 인터페이스(UI)를 여러 언어로 제공할 수 있습니다. 이번 포스트에서는 플러터에서 국제화를 구현하는 방법에 대해 알아보겠습니다.

## 단계 1: 프로젝트 설정 변경

프로젝트의 `pubspec.yaml` 파일을 열어 dependencies 섹션에 `flutter_localizations` 패키지를 추가합니다. 아래와 같이 작성합니다.

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter
```

설정 변경 후, 터미널에서 `flutter packages get` 명령을 실행하여 패키지를 다운로드합니다.

## 단계 2: 지원할 언어 파일 준비

프로젝트의 루트 디렉토리에 `lib` 폴더 안에 `l10n` 폴더를 생성합니다. 그리고 `l10n` 폴더 안에 `intl_en.arb`, `intl_ko.arb`와 같이 각 언어별 파일을 준비합니다.

각 언어 파일은 [ARBT(Translation File Format)](https://github.com/flutter/flutter/blob/main/packages/flutter_localizations/lib/src/l10n/arb_en.arb) 형식으로 작성됩니다. 예를 들어 `intl_en.arb` 파일에는 아래와 같이 작성할 수 있습니다.

```json
{
  "@@locale": "en",
  "title": "Welcome to my app",
  "hello": "Hello!",
  "button_text": "Click Me"
}
```

위와 같이 `@@locale`은 언어 코드를 나타내고, `"title": "Welcome to my app"`과 같이 각 키와 값이 쌍으로 작성됩니다.

## 단계 3: 국제화 설정 추가

`lib` 폴더에 `l10n.dart` 파일을 생성하고, 아래와 같이 작성합니다.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_localizations/flutter_localizations.dart';

class AppLocalizations {
  static const LocalizationsDelegate delegate = _AppLocalizationsDelegate();

  static AppLocalizations of(BuildContext context) {
    return Localizations.of<AppLocalizations>(context, AppLocalizations);
  }

  String get title {
    return "Welcome to my app";
  }

  String get hello {
    return "Hello!";
  }

  String get buttonText {
    return "Click Me";
  }
}

class _AppLocalizationsDelegate extends LocalizationsDelegate<AppLocalizations> {
  const _AppLocalizationsDelegate();

  @override
  bool isSupported(Locale locale) {
    return ['en', 'ko'].contains(locale.languageCode);
  }

  @override
  Future<AppLocalizations> load(Locale locale) {
    return SynchronousFuture<AppLocalizations>(AppLocalizations());
  }

  @override
  bool shouldReload(_AppLocalizationsDelegate old) {
    return false;
  }
}

```

이제 `main.dart` 파일에서 `MaterialApp` 위젯에 `localizationsDelegates`와 `supportedLocales`를 추가합니다.

```dart
import 'package:flutter/material.dart';
import 'l10n.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      localizationsDelegates: [
        AppLocalizations.delegate,
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
      ],
      supportedLocales: [
        const Locale('en', ''),
        const Locale('ko', ''),
      ],
      title: 'Internationalization Example',
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final AppLocalizations localizations = AppLocalizations.of(context);

    return Scaffold(
      appBar: AppBar(
        title: Text(localizations.title),
      ),
      body: Center(
        child: Text(localizations.hello),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          showDialog(
            context: context,
            builder: (BuildContext context) {
              return AlertDialog(
                title: Text(localizations.buttonText),
                actions: <Widget>[
                  FlatButton(
                    child: Text('OK'),
                    onPressed: () {
                      Navigator.of(context).pop();
                    },
                  ),
                ],
              );
            },
          );
        },
        child: Icon(Icons.add),
      ),
    );
  }
}
```

## 단계 4: 언어 변경 테스트

이제 앱을 실행하고 언어를 변경하여 확인해보세요. `supportedLocales`에 추가한 언어 코드에 따라 앱의 UI가 해당 언어로 변경될 것입니다.

## 결론

플러터에서 국제화를 구현하는 방법을 알아보았습니다. 플러터의 국제화 기능을 활용하여 다국어 지원 앱을 쉽게 개발할 수 있습니다. 추가적으로 `l10n` 폴더 안에 지원할 언어별 파일을 작성하여 다양한 언어로 앱을 제공할 수 있습니다.