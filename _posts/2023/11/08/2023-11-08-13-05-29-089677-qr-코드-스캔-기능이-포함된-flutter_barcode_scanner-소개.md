---
layout: post
title: "[flutter] QR 코드 스캔 기능이 포함된 flutter_barcode_scanner 소개"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

## 소개
flutter_barcode_scanner는 QR 코드 스캔 기능을 구현하기 위해 사용할 수 있는 Flutter 패키지입니다. 이 패키지를 사용하면 간단하게 QR 코드를 스캔하고 정보를 추출할 수 있습니다.

## 설치
flutter_barcode_scanner를 사용하려면 프로젝트의 `pubspec.yaml` 파일에 다음과 같은 의존성을 추가해야 합니다:

```yaml
dependencies:
  flutter_barcode_scanner: ^2.0.0
```

의존성을 추가한 후, `flutter pub get` 명령을 실행하여 패키지를 설치합니다.

## 사용법
`flutter_barcode_scanner` 패키지를 사용하여 QR 코드 스캔을 수행하는 예제 코드는 다음과 같습니다:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_barcode_scanner/flutter_barcode_scanner.dart';

class QRCodeScannerScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('QR Code Scanner'),
      ),
      body: Center(
        child: RaisedButton(
          child: Text('Start QR Scan'),
          onPressed: () async {
            String qrCode = await FlutterBarcodeScanner.scanBarcode(
              '#ff6666', // 스캔 화면의 배경 색상 설정
              'Cancel', // 취소 버튼 텍스트 설정
              true, // 바코드 또는 QR 코드 중 하나만 스캔할지 여부 설정
              ScanMode.QR, // 스캔 모드 설정 (바코드 또는 QR 코드)
            );

            if (qrCode != '-1') {
              // 스캔된 QR 코드를 사용하여 원하는 작업 수행
              print('Scanned QR code: $qrCode');
            }
          },
        ),
      ),
    );
  }
}
```

위 예제 코드에서 `FlutterBarcodeScanner.scanBarcode()` 메서드를 사용하여 QR 코드 스캔을 수행합니다. 스캔이 완료되면 스캔된 QR 코드가 반환되고, 취소되거나 오류가 발생한 경우 `-1`이 반환됩니다.

## 참고 자료
- [flutter_barcode_scanner 패키지](https://pub.dev/packages/flutter_barcode_scanner)
- [flutter_barcode_scanner GitHub 저장소](https://github.com/flutter/flutter_barcode_scanner)