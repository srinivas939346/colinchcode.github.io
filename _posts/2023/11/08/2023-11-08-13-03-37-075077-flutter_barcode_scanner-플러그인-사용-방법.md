---
layout: post
title: "[flutter] flutter_barcode_scanner 플러그인 사용 방법"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

flutter_barcode_scanner 플러그인은 Flutter 앱에서 바코드 스캔을 수행하는 데 사용되는 플러그인입니다. 이 플러그인을 사용하여 사용자의 디바이스 카메라로부터 바코드를 스캔하고 해당 바코드에 대한 정보를 얻을 수 있습니다. 이 글에서는 flutter_barcode_scanner 플러그인을 설치하고 사용하는 방법에 대해 알아보겠습니다.

## 1. flutter_barcode_scanner 플러그인 설치하기

먼저, `pubspec.yaml` 파일을 열고 `dependencies` 섹션에 다음과 같은 코드를 추가합니다:

```yaml
dependencies:
  flutter_barcode_scanner: ^2.1.0
```

그런 다음 터미널에서 다음 명령을 실행하여 플러그인을 설치합니다:

```bash
flutter pub get
```

## 2. flutter_barcode_scanner 사용하기

flutter_barcode_scanner를 사용하기 위해 먼저 해당 플러그인을 import해야 합니다. 다음과 같이 `main.dart` 파일의 상단에 import 문을 추가합니다:

```dart
import 'package:flutter_barcode_scanner/flutter_barcode_scanner.dart';
```

바코드를 스캔하려는 버튼이 있는 위젯을 만들고 해당 버튼이 클릭되었을 때 바코드 스캔을 호출하도록 코드를 작성합니다. 예를 들어, 다음과 같이 코드를 작성할 수 있습니다:

```dart
FlatButton(
  onPressed: () async {
    String barcodeScanResult = await FlutterBarcodeScanner.scanBarcode(
      "#ff6666",
      "Cancel",
      false,
      ScanMode.DEFAULT,
    );

    setState(() {
      // 스캔 결과 처리
    });
  },
  child: Text(
    "바코드 스캔하기",
    style: TextStyle(fontSize: 18),
  ),
)
```

`scanBarcode` 함수는 다음 매개변수들을 받습니다:
- `#ff6666`: 스캔화면 상단의 색상을 설정합니다.
- `Cancel`: 취소 버튼의 텍스트를 설정합니다.
- `false`: 스캔 성공 시 화면이 유지되는지 결정합니다.
- `ScanMode.DEFAULT`: 스캔 모드를 설정합니다.

바코드 스캔 결과는 `barcodeScanResult` 변수에 담기게 되며, 해당 변수를 통해 스캔된 바코드에 대한 정보를 얻을 수 있습니다.

## 3. 플러그인 사용 시 주의할 점

- `flutter_barcode_scanner` 플러그인은 Android와 iOS에서만 동작합니다.
- Android의 경우, 카메라 접근 권한이 필요합니다. 따라서 `AndroidManifest.xml` 파일에 `android.permission.CAMERA` 퍼미션을 추가해야 합니다.
- iOS의 경우, `Info.plist` 파일에 `NSCameraUsageDescription` 키를 추가하고 권한에 대한 설명을 작성해야 합니다.

이상으로 flutter_barcode_scanner 플러그인의 설치와 사용 방법에 대해 알아보았습니다. 여러분은 이 플러그인을 사용하여 Flutter 앱에서 바코드 스캔 기능을 추가할 수 있습니다.

[flutter_barcode_scanner GitHub 페이지](https://github.com/AmruthPillai/FlutterBarcodeScanner)

참고: 
- [flutter_barcode_scanner 플러그인 문서](https://pub.dev/packages/flutter_barcode_scanner)
- [Flutter 설치 가이드](https://flutter.dev/docs/get-started/install)