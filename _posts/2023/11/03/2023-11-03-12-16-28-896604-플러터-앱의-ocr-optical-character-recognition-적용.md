---
layout: post
title: "[flutter] 플러터 앱의 OCR (Optical Character Recognition) 적용"
description: " "
date: 2023-11-03
tags: [flutter]
comments: true
share: true
---

안녕하세요! 오늘은 플러터(Flutter) 앱에 OCR (Optical Character Recognition)을 적용하는 방법에 대해 알아보겠습니다.

OCR은 이미지에서 텍스트를 추출하여 인식하는 기술로, 다양한 용도로 사용됩니다. 예를 들면, 사진에서 주소를 추출하거나, 명함의 정보를 가져오는 등 다양한 경우에 활용할 수 있습니다.

## 1. 플러터에서 OCR을 지원하는 패키지 찾기

플러터에서는 다양한 OCR 패키지를 제공하고 있습니다. 이 중에서 사용하기 편한 패키지를 선택하여 적용해보도록 하겠습니다. 일반적으로 사용되는 패키지로는 Firebase ML Kit, Tesseract 등이 있습니다.

Firebase ML Kit의 경우, Firebase 프로젝트를 설정해야 하므로 추가적인 작업이 필요할 수 있습니다. Tesseract는 오픈 소스 기반의 패키지이며, 플러터에서 사용하기 쉽습니다. 본 예제에서는 Tesseract를 사용하여 OCR을 적용하도록 하겠습니다.

## 2. Tesseract OCR 패키지 추가하기

플러터 프로젝트에 Tesseract OCR 패키지를 추가하기 위해서는 `flutter_tesseract_ocr` 패키지를 사용하면 됩니다.

1. `pubspec.yaml` 파일을 열고, `dependencies` 섹션에 아래와 같이 패키지를 추가합니다.

   ```yaml
   dependencies:
     flutter_tesseract_ocr: ^3.0.0
   ```

2. 터미널에서 `flutter packages get` 명령어를 실행하여 패키지를 다운로드 받습니다.

## 3. OCR 로직 구현하기

Tesseract OCR을 사용하여 텍스트를 추출하는 로직을 구현해보겠습니다.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_tesseract_ocr/flutter_tesseract_ocr.dart';

class OCRScreen extends StatefulWidget {
  @override
  _OCRScreenState createState() => _OCRScreenState();
}

class _OCRScreenState extends State<OCRScreen> {
  String extractedText = '';

  Future<void> performOCR() async {
    final imagePath = 'path_to_image.jpg'; // OCR을 적용할 이미지 경로
    final extracted = await FlutterTesseractOcr.extractText(imagePath);
    setState(() {
      extractedText = extracted;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('OCR Screen'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            RaisedButton(
              onPressed: performOCR,
              child: Text('Apply OCR'),
            ),
            SizedBox(height: 20),
            Text(
              'Extracted Text:',
              style: TextStyle(
                fontSize: 18,
                fontWeight: FontWeight.bold,
              ),
            ),
            SizedBox(height: 10),
            Text(extractedText),
          ],
        ),
      ),
    );
  }
}
```

위의 코드에서 `performOCR` 메소드에서는 OCR을 적용할 이미지의 경로를 지정하고, `FlutterTesseractOcr.extractText`를 사용하여 텍스트를 추출합니다. 추출된 텍스트는 `extractedText` 변수에 저장되고, 화면에 표시됩니다.

## 4. OCR 화면 호출하기

OCR을 적용하고자 하는 화면에서 `OCRScreen` 위젯을 호출하여 OCR 화면을 표시해야 합니다. 예를 들어, 버튼을 누를 때 OCR 화면으로 이동하도록 구현할 수 있습니다.

예시 코드:

```dart
RaisedButton(
  onPressed: () {
    Navigator.push(
      context,
      MaterialPageRoute(builder: (context) => OCRScreen()),
    );
  },
  child: Text('Go to OCR Screen'),
),
```

위 예시 코드에서는 버튼을 누르면 `OCRScreen`으로 이동하는 동작을 구현하였습니다.

## 마무리

이제 앱 내에서 OCR을 적용하여 이미지에서 텍스트를 추출할 수 있는 기능을 구현했습니다. Tesseract OCR 패키지를 사용하여 플러터 앱에 OCR 기능을 쉽게 추가할 수 있으니, 필요한 경우 활용하시기 바랍니다.

더 자세한 내용은 [pub.dev](https://pub.dev/)에서 `flutter_tesseract_ocr` 패키지와 관련 문서를 참고하실 수 있습니다.