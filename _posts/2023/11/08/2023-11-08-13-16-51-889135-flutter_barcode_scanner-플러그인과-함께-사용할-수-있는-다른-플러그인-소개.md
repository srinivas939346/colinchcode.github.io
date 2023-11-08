---
layout: post
title: "[flutter] flutter_barcode_scanner 플러그인과 함께 사용할 수 있는 다른 플러그인 소개"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

이번에는 Flutter 애플리케이션에서 바코드 스캐닝 기능을 구현할 수 있는 플러그인인 `flutter_barcode_scanner`와 함께 사용할 수 있는 다른 유용한 플러그인들을 소개하고자 합니다. 바코드 스캐너는 제품의 바코드를 스캔하여 제품 정보를 파악하거나, 이벤트 참가자의 QR 코드를 스캔하여 등록하는 등 다양한 용도로 활용할 수 있습니다.

## 1. flutter_camera_ml_vision

이 플러그인은 ML Kit Vision API를 활용하여 카메라가 촬영한 영상에서 바코드를 실시간으로 감지하고 인식하는 기능을 제공합니다. 이를 통해 사용자가 카메라를 향해 바코드를 비추면 자동으로 인식하여 결과를 반환할 수 있습니다.

**사용 예시 코드:**

```dart
import 'package:flutter_camera_ml_vision/flutter_camera_ml_vision.dart';

class BarcodeScannerWidget extends StatefulWidget {
  @override
  _BarcodeScannerWidgetState createState() => _BarcodeScannerWidgetState();
}

class _BarcodeScannerWidgetState extends State<BarcodeScannerWidget> {
  List<Barcode> _barcodes = [];

  @override
  Widget build(BuildContext context) {
    return CameraMlVision<List<Barcode>>(
      detector: vision.barcodeDetector(),
      onResult: (barcodes) {
        setState(() {
          _barcodes = barcodes;
        });
      },
      cameraLensDirection: CameraLensDirection.back,
    );
  }
}
```

## 2. qr_code_scanner

`qr_code_scanner` 플러그인은 바코드 스캐너 외에도 QR 코드를 스캔하는 기능을 제공합니다. QR 코드는 저작권 정보, URL, 연락처 등 다양한 정보를 포함할 수 있으며, 이 플러그인을 사용하면 Flutter 애플리케이션에서 손쉽게 QR 코드를 스캔하여 해당 정보에 접근할 수 있습니다.

**사용 예시 코드:**

```dart
import 'package:qr_code_scanner/qr_code_scanner.dart';

class QRCodeScannerWidget extends StatefulWidget {
  @override
  _QRCodeScannerWidgetState createState() => _QRCodeScannerWidgetState();
}

class _QRCodeScannerWidgetState extends State<QRCodeScannerWidget> {
  final GlobalKey qrKey = GlobalKey(debugLabel: 'QR');

  QRViewController? _controller;
  String? _qrText = '';

  @override
  Widget build(BuildContext context) {
    return Stack(
      children: [
        QRView(
          key: qrKey,
          onQRViewCreated: _onQRViewCreated,
        ),
        Positioned(
          bottom: 16,
          left: 16,
          child: Text(_qrText!),
        ),
      ],
    );
  }

  void _onQRViewCreated(QRViewController controller) {
    setState(() {
      _controller = controller;
      controller.scannedDataStream.listen((scanData) {
        setState(() {
          _qrText = scanData.code;
        });
      });
    });
  }

  @override
  void dispose() {
    _controller?.dispose();
    super.dispose();
  }
}
```

## 3. barcode_widget

`barcode_widget`은 바코드 및 QR 코드 스캔까지는 필요하지 않지만, 스캔한 결과를 간편하게 화면에 표시하기 위한 위젯을 제공하는 플러그인입니다. 이를 사용하면 스캔된 바코드 또는 QR 코드 정보를 깔끔하게 UI에 표시할 수 있습니다.

**사용 예시 코드:**

```dart
import 'package:barcode_widget/barcode_widget.dart';

class BarcodeDisplayWidget extends StatelessWidget {
  final String barcodeData;

  BarcodeDisplayWidget(this.barcodeData);

  @override
  Widget build(BuildContext context) {
    return Center(
      child: BarcodeWidget(
        barcode: Barcode.qrCode(),
        data: barcodeData,
        width: 200,
        height: 200,
        style: BarcodeStyle(
          lineColor: Colors.black,
          lineWidth: 2,
        ),
      ),
    );
  }
}
```

위에서 소개한 플러그인들은 `flutter_barcode_scanner`와 함께 사용할 수 있으며, 각각의 특징과 사용법을 잘 숙지하여 원하는 기능을 구현할 수 있도록 활용해보세요.

> 참고 자료:
> - [flutter_camera_ml_vision 플러그인](https://pub.dev/packages/flutter_camera_ml_vision)
> - [qr_code_scanner 플러그인](https://pub.dev/packages/qr_code_scanner)
> - [barcode_widget 플러그인](https://pub.dev/packages/barcode_widget)