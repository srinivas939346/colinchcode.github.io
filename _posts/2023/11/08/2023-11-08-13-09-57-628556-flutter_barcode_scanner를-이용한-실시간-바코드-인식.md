---
layout: post
title: "[flutter] flutter_barcode_scanner를 이용한 실시간 바코드 인식"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

## 소개

이 튜토리얼에서는 Flutter 앱에서 실시간으로 바코드를 인식하는 방법을 알아보겠습니다. flutter_barcode_scanner를 사용하여 바코드를 스캔하고 결과를 처리하는 간단한 예제를 만들어볼 것입니다.

## 준비사항

- Flutter 개발 환경이 설치되어 있어야 합니다.

## flutter_barcode_scanner 설치

flutter_barcode_scanner는 바코드 스캐너를 쉽게 사용할 수 있도록 도와주는 플러그인입니다. 아래의 명령을 실행하여 flutter_barcode_scanner를 설치합니다.

```shell
flutter pub add flutter_barcode_scanner
```

또는 `pubspec.yaml` 파일에 직접 의존성을 추가할 수 있습니다.

```yaml
dependencies:
  flutter_barcode_scanner: ^3.0.0
```

추가한 후에는 `flutter pub get` 명령을 실행하여 종속성을 가져옵니다.

## 바코드 스캐너 사용하기

### 1. flutter_barcode_scanner 패키지 가져오기

먼저, 바코드 스캐너를 사용하기 위해 `flutter_barcode_scanner` 패키지를 가져옵니다.

```dart
import 'package:flutter_barcode_scanner/flutter_barcode_scanner.dart';
```

### 2. 바코드 스캔 기능 구현하기

다음으로, 바코드를 스캔하는 기능을 구현합니다. 예를 들어, 버튼을 누르면 바코드 스캔이 시작되도록할 것입니다.

```dart
FlatButton(
  onPressed: () async {
    String barcode = await FlutterBarcodeScanner.scanBarcode(
      '#FF0000', // 바코드 스캔 화면의 색상 설정
      'Cancel', // 취소 버튼 텍스트 설정
      false, // 디바이스 플래시 사용 여부 설정
      ScanMode.BARCODE, // 바코드 스캔 모드 설정
    );

    // 바코드 결과 처리
    setState(() {
      _barcode = barcode;
    });
  },
  child: Text('바코드 스캔'),
)
```

### 3. 바코드 결과 처리하기

바코드 스캔이 완료되면, 스캔한 바코드의 결과를 처리할 수 있습니다. 예제에서는 `_barcode` 변수에 스캔한 바코드의 결과를 저장합니다.

```dart
String _barcode = '';

Text('스캔 결과: $_barcode')
```

## 결론

이제, Flutter 앱에서 실시간으로 바코드를 인식하는 방법을 알았습니다. 이를 통해 여러 가지 앱 개발 시나리오에서 바코드 스캔 기능을 활용할 수 있습니다.

더 자세한 내용은 [flutter_barcode_scanner 공식 문서](https://pub.dev/packages/flutter_barcode_scanner)를 참조하세요.