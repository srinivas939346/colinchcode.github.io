---
layout: post
title: "[flutter] 플러터(Flutter)에서 앱 베지에이션(App Localization) 구현하기"
description: " "
date: 2023-11-03
tags: [flutter]
comments: true
share: true
---

플러터(Flutter)는 네이티브 앱을 개발하기 위한 뛰어난 프레임워크로 앱의 다국어 지원을 제공합니다. 이를 통해 앱 베지에이션(App Localization)을 쉽게 구현할 수 있습니다. 이번 튜토리얼에서는 플러터에서 앱 베지에이션을 구현하는 방법을 알아보겠습니다.

---

## 목차

1. [앱 베지에이션 패키지 설치](#앱-베지에이션-패키지-설치)
2. [다국어 리소스 파일 생성](#다국어-리소스-파일-생성)
3. [로캘 변경하기](#로캘-변경하기)
4. [텍스트 문자열 추출](#텍스트-문자열-추출)
5. [사용자의 로캘 설정](#사용자의-로캘-설정)
6. [결론](#결론)

---

## 1. 앱 베지에이션 패키지 설치

첫 번째로, 앱 베지에이션을 구현하기 위해 `flutter_localizations` 패키지를 프로젝트에 추가해야 합니다. `pubspec.yaml` 파일에 아래와 같이 패키지를 추가합니다:

```yaml
dependencies:
  flutter_localizations:
    sdk: flutter
```

설정을 완료한 후에는 패키지를 설치해야 합니다:

```shell
$ flutter packages get
```

---

## 2. 다국어 리소스 파일 생성

다음으로, 앱에 사용될 다국어 리소스 파일을 생성해야 합니다. `lib` 폴더 내부에 `l10n` 폴더를 생성한 뒤, 그 안에 `intl_messages.arb` 파일을 만듭니다. 이 파일에는 앱에서 사용될 모든 문자열을 포함시킬 것입니다.

예를 들어, 다음과 같이 `intl_messages.arb` 파일을 작성합니다:

```json
{
  "appName": "Flutter 앱",
  "@appName": {
    "description": "앱의 이름",
    "type": "text"
  },
  "welcomeMessage": "환영합니다!",
  "@welcomeMessage": {
    "description": "앱 시작 화면에 표시되는 환영 메시지",
    "type": "text"
  },
  ...
}
```

---

## 3. 로캘 변경하기

이제 앱 내에서 로캘을 변경할 수 있는 방법을 구현해야 합니다. 앱에서 로캘을 변경하면 앱의 텍스트 문자열이 해당 로캘에 맞춰 업데이트됩니다.

다음은 로캘을 변경하는 간단한 코드 예제입니다:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_localizations/flutter_localizations.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      localizationsDelegates: [
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
      ],
      supportedLocales: [
        const Locale('en', ''),
        const Locale('ko', ''),
      ],
      localeResolutionCallback: (locale, supportedLocales) {
        for (var supportedLocale in supportedLocales) {
          if (supportedLocale.languageCode == locale.languageCode &&
              supportedLocale.countryCode == locale.countryCode) {
            return supportedLocale;
          }
        }
        return supportedLocales.first;
      },
      title: 'Flutter Localization',
      home: MyHomePage(),
    );
  }
}
```

---

## 4. 텍스트 문자열 추출

다음으로, 앱 내에서 사용되는 텍스트 문자열을 추출해야 합니다. 이를 위해 `flutter_localizations`를 사용할 것입니다.

앱 내에서 텍스트 문자열을 추출하기 위해 `Intl` 패키지를 사용합니다. 다음은 추출 기능을 사용하는 예제 코드입니다:

```dart
import 'package:flutter/material.dart';
import 'package:intl/intl.dart';

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    Intl.defaultLocale = Localizations.localeOf(context).languageCode;

    return Scaffold(
      appBar: AppBar(
        title: Text(Intl.message(
          'appName',
          name: 'appName',
        )),
      ),
      body: Center(
        child: Text(Intl.message(
          'welcomeMessage',
          name: 'welcomeMessage',
        )),
      ),
    );
  }
}
```

---

## 5. 사용자의 로캘 설정

마지막으로, 앱에서 사용자의 로캘 설정을 관리할 수 있도록 해야 합니다. 사용자는 앱 내에서 로캘을 변경하고, 선택한 로캘이 앱 전체에 적용되도록 해야 합니다.

이를 위해 `SharedPreferences` 패키지를 사용할 수 있습니다. 다음은 사용자의 로캘을 저장하고 불러오는 예제 코드입니다:

```dart
import 'package:shared_preferences/shared_preferences.dart';

class LocaleManager {
  static const String selectedLocaleKey = 'selectedLocale';

  static Future<Locale> getSelectedLocale() async {
    SharedPreferences preferences = await SharedPreferences.getInstance();
    String selectedLocale = preferences.getString(selectedLocaleKey);
    return Locale(selectedLocale);
  }

  static Future<void> setSelectedLocale(Locale locale) async {
    SharedPreferences preferences = await SharedPreferences.getInstance();
    preferences.setString(selectedLocaleKey, locale.languageCode);
  }
}
```

---

## 결론

플러터(Flutter)를 사용하여 앱의 다국어 지원을 구현하는 방법에 대해 알아보았습니다. 앱 베지에이션을 구현하면 사용자가 선택한 로캘에 맞춰 앱 내의 텍스트 문자열을 자동으로 업데이트할 수 있습니다. 플러터의 다양한 기능과 패키지를 활용하여 사용자 친화적인 앱을 개발할 수 있습니다.

더 많은 정보를 찾으려면 플러터 공식 문서를 참조해주세요.

- [Flutter 공식 웹사이트](https://flutter.dev/)
- [Flutter 다국어 지원 가이드](https://flutter.dev/docs/development/accessibility-and-localization/internationalization)