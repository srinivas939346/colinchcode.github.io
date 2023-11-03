---
layout: post
title: "[flutter] 플러터(Flutter)에서 푸시 알림(Push Notification) 구현하기"
description: " "
date: 2023-11-03
tags: [flutter]
comments: true
share: true
---

플러터(Flutter)는 다양한 플랫폼에서 동작하는 모바일 애플리케이션을 개발하기 위한 프레임워크입니다. 푸시 알림(Push Notification)은 사용자에게 중요한 메시지나 업데이트를 전달하기 위해 매우 유용한 기능입니다. 이번 글에서는 플러터에서 푸시 알림을 구현하는 방법에 대해 알아보겠습니다.

## 1. Firebase 설정하기

Firebase는 구글에서 제공하는 모바일 애플리케이션 개발 플랫폼으로, 푸시 알림을 구현하기 위해 사용됩니다. 따라서 먼저 Firebase에 프로젝트를 생성하고 설정해야 합니다.

1. Firebase 콘솔에 접속하여 프로젝트를 생성합니다.
2. 생성한 프로젝트에서 '프로젝트 설정'을 클릭합니다.
3. '클라우드 메시징' 탭으로 이동하여 FCM 서버 키를 확인합니다.

## 2. 플러터 앱에 Firebase 통합하기

1. FlutterFire를 사용하여 플러터 앱에 Firebase를 통합합니다. `pubspec.yaml` 파일에 다음 의존성을 추가합니다:
   ```dart
   dependencies:
     flutter:
       sdk: flutter
     firebase_core: ^1.0.0
     firebase_messaging: ^10.0.0
   ```
2. 터미널에서 `flutter pub get` 명령을 실행하여 의존성을 설치합니다.
3. `main.dart` 파일에서 Firebase를 초기화합니다:
   ```dart
   import 'package:firebase_core/firebase_core.dart';

   Future<void> main() async {
     WidgetsFlutterBinding.ensureInitialized();
     await Firebase.initializeApp();
     runApp(MyApp());
   }
   ```

## 3. 푸시 알림 받기

1. `main.dart` 파일에 푸시 알림을 처리하는 코드를 추가합니다:
   ```dart
   import 'package:firebase_messaging/firebase_messaging.dart';

   void main() async {
     // ...

     FirebaseMessaging.onMessage.listen((RemoteMessage message) {
       // 앱이 foreground 상태일 때 푸시 알림을 받은 경우 처리 로직
     });

     FirebaseMessaging.onBackgroundMessage(_onBackgroundMessageHandler);

     // ...
   }
   ```

## 4. 백그라운드에서 푸시 알림 처리

백그라운드에서 푸시 알림을 처리하기 위해 `onBackgroundMessage` 핸들러를 정의해야 합니다.

```dart
Future<void> _onBackgroundMessageHandler(RemoteMessage message) async {
  // 앱이 백그라운드에 있는 경우 푸시 알림을 받은 경우 처리 로직
}
```

## 5. FCM 서버 키 설정

1. 푸시 알림을 보내기 위해 FCM 서버 키를 사용해야 합니다. `main.dart` 파일에 FCM 서버 키를 설정합니다:
   ```dart
   await FirebaseMessaging.instance.setForegroundNotificationPresentationOptions(
     alert: true,
     badge: true,
     sound: true,
   );
   ```

## 6. 푸시 알림 테스트

이제 구현한 푸시 알림을 테스트해볼 차례입니다. Firebase 콘솔에서 앱의 디바이스 토큰을 확인하고, 푸시 알림을 전송하여 앱이 잘 동작하는지 확인할 수 있습니다.

## 마무리

이번 글에서는 플러터(Flutter)에서 푸시 알림(Push Notification)을 구현하는 방법에 대해 알아보았습니다. Firebase를 통해 쉽게 푸시 알림을 처리할 수 있으므로, 앱의 사용성을 향상시키기 위해 푸시 알림 기능을 적극 활용해보시기 바랍니다.

더 자세한 내용은 [Firebase 공식 문서](https://firebase.google.com/docs/flutter/setup)를 참고하시기 바랍니다.