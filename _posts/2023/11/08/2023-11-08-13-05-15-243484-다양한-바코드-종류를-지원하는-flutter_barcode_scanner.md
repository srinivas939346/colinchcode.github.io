---
layout: post
title: "[flutter] 다양한 바코드 종류를 지원하는 flutter_barcode_scanner"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

플러터(Flutter)는 크로스 플랫폼 모바일 애플리케이션 개발을 위한 인기있는 프레임워크입니다. 바코드 스캐너는 많은 애플리케이션에서 중요한 기능 중 하나입니다. flutter_barcode_scanner는 플러터 애플리케이션에서 다양한 바코드 종류를 스캔할 수 있도록 도와주는 라이브러리입니다.

## flutter_barcode_scanner 소개

flutter_barcode_scanner는 Flutter와 함께 사용되는 오픈 소스 바코드 스캐너 라이브러리입니다. 이 라이브러리는 앱 개발자가 플러터 프로젝트에 바코드 스캐너 기능을 간단하게 추가할 수 있도록 지원합니다. flutter_barcode_scanner는 다양한 바코드 종류를 지원하며, QR 코드, UPC 코드, EAN 코드 등을 스캔할 수 있습니다.

## 설치 방법

flutter_barcode_scanner 라이브러리를 사용하기 위해서는 먼저 플러터 프로젝트에 해당 라이브러리를 추가해야 합니다. 다음의 단계를 따라 진행해보세요.

1. 터미널 또는 명령 프롬프트를 열고 플러터 프로젝트 디렉토리로 이동합니다.
2. 다음 명령을 실행하여 flutter_barcode_scanner 패키지를 추가합니다.

   ```dart
   flutter pub add flutter_barcode_scanner
   ```
   
   혹은 `pubspec.yaml` 파일에 패키지를 직접 추가할 수도 있습니다.
   
   ```yaml
   dependencies:
     flutter_barcode_scanner: ^3.0.0
   ```

3. 패키지를 프로젝트에 적용하기 위해 아래 명령을 실행합니다.

   ```dart
   flutter pub get
   ```

## 사용 방법

flutter_barcode_scanner를 사용하여 플러터 애플리케이션에 바코드 스캐너를 추가해보겠습니다.

1. 앱의 `main.dart` 파일을 열고 다음의 코드를 추가합니다.

   ```dart
   import 'package:flutter/material.dart';
   import 'package:flutter_barcode_scanner/flutter_barcode_scanner.dart';
   
   void main() {
     runApp(MyApp());
   }
   
   class MyApp extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return MaterialApp(
         title: 'Barcode Scanner',
         home: BarcodeScannerPage(),
       );
     }
   }
   
   class BarcodeScannerPage extends StatefulWidget {
     @override
     _BarcodeScannerPageState createState() => _BarcodeScannerPageState();
   }
   
   class _BarcodeScannerPageState extends State<BarcodeScannerPage> {
     String _scanResult = "스캔 결과 없음";
   
     Future<void> _scanBarcode() async {
       String scanResult = await FlutterBarcodeScanner.scanBarcode(
           "#ff6666", "취소", true, ScanMode.BARCODE);
   
       setState(() {
         _scanResult = scanResult;
       });
     }
   
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         appBar: AppBar(
           title: Text('Barcode Scanner'),
         ),
         body: Center(
           child: Column(
             mainAxisAlignment: MainAxisAlignment.center,
             children: <Widget>[
               Text(
                 '스캔 결과:',
               ),
               Text(
                 _scanResult,
                 style: TextStyle(
                   fontSize: 20.0,
                   fontWeight: FontWeight.bold,
                 ),
               ),
             ],
           ),
         ),
         floatingActionButton: FloatingActionButton(
           onPressed: _scanBarcode,
           tooltip: '스캔',
           child: Icon(Icons.qr_code_scanner),
         ),
       );
     }
   }
   ```
   
   이 코드는 플러터 앱의 메인 화면에 바코드 스캐너 버튼과 스캔 결과를 보여주는 기능을 추가합니다.
   
2. 앱을 실행하여 바코드 스캐너를 테스트해보세요.

## 결론

flutter_barcode_scanner는 플러터 프로젝트에서 쉽게 사용할 수 있는 바코드 스캐너 라이브러리입니다. QR 코드부터 EAN 코드까지 다양한 종류의 바코드를 스캔할 수 있습니다. 위의 가이드를 따라 설치 및 사용 방법을 알아보고, 해당 기능을 앱에 추가해보세요.

### 참고 자료

- [flutter_barcode_scanner GitHub 저장소](https://github.com/flutter/flutter_barcode_scanner)
- [플러터(Flutter) 공식 사이트](https://flutter.dev/)