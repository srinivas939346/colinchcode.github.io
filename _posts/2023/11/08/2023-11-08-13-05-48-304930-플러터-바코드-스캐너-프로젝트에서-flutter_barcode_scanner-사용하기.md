---
layout: post
title: "[flutter] 플러터 바코드 스캐너 프로젝트에서 flutter_barcode_scanner 사용하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

플러터(Flutter)는 다양한 기능을 제공하는 플랫폼이며, 바코드 스캐너 기능이 필요한 경우 `flutter_barcode_scanner` 패키지를 사용할 수 있습니다. 이 패키지는 플러터 앱에서 바코드를 스캔하는 기능을 구현하는 데 도움을 줍니다.

## `flutter_barcode_scanner` 패키지 설치하기

먼저 `pubspec.yaml` 파일에 `flutter_barcode_scanner` 패키지를 추가해야 합니다. 다음과 같이 `dependencies` 섹션에 패키지를 추가합니다:

```yaml
dependencies:
  flutter_barcode_scanner: ^3.0.0
```

이후 터미널에서 `flutter pub get` 명령어를 실행하여 패키지를 설치합니다.

## 바코드 스캐너 구현하기

다음은 간단한 바코드 스캐너를 구현하는 예시입니다. `flutter_barcode_scanner` 패키지의 `FlutterBarcodeScanner` 클래스를 사용하여 스캐너를 호출하고, 스캔 결과를 처리하는 메소드를 작성합니다.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_barcode_scanner/flutter_barcode_scanner.dart';

class BarcodeScannerPage extends StatefulWidget {
  @override
  _BarcodeScannerPageState createState() => _BarcodeScannerPageState();
}

class _BarcodeScannerPageState extends State<BarcodeScannerPage> {
  String _scanResult = '';

  Future<void> _scanBarcode() async {
    String scanResult = await FlutterBarcodeScanner.scanBarcode(
      '#ff6666', // 툴바 및 상태 표시줄의 색상
      '취소', // 취소 버튼 텍스트
      true, // 스캐너의 특수 기능 활성화 여부
      ScanMode.BARCODE, // 스캔 모드
    );

    setState(() {
      _scanResult = scanResult;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('바코드 스캐너'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              '스캔 결과:',
              style: TextStyle(fontSize: 18),
            ),
            SizedBox(height: 10),
            Text(
              _scanResult,
              style: TextStyle(fontSize: 24, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 20),
            RaisedButton(
              child: Text('스캔 시작'),
              onPressed: _scanBarcode,
            ),
          ],
        ),
      ),
    );
  }
}

```

이 예시 코드에서는 `BarcodeScannerPage` 클래스에 `FlutterBarcodeScanner` 패키지를 사용하여 `_scanBarcode` 메소드를 구현했습니다. 이 메소드는 `await FlutterBarcodeScanner.scanBarcode(...)`를 호출하여 바코드를 스캔하고, 결과를 `_scanResult` 변수에 저장합니다.

또한, `build` 메소드에서는 `_scanResult` 변수를 UI에 표시하고, `RaisedButton` 위젯을 통해 바코드 스캔을 시작할 수 있도록 구성했습니다.

## 실행 결과 확인하기

이제 앱을 실행하면 `스캔 시작` 버튼을 클릭하여 바코드를 스캔할 수 있습니다. 스캔된 결과는 화면에 표시되며, `_scanResult` 변수에도 저장됩니다.

바코드 스캐너 기능을 플러터 앱에 쉽게 추가할 수 있는 `flutter_barcode_scanner` 패키지를 사용하여 편리하게 바코드 스캐너 앱을 개발해보세요.