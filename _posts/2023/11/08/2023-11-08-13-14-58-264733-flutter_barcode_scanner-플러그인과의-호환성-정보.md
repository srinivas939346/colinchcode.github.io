---
layout: post
title: "[flutter] flutter_barcode_scanner 플러그인과의 호환성 정보"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

## 소개

이번 포스트에서는 Flutter에서 사용되는 `flutter_barcode_scanner` 플러그인의 호환성 정보를 알려드리겠습니다. `flutter_barcode_scanner` 플러그인은 카메라를 사용하여 바코드를 스캔하는 기능을 제공합니다. 따라서 해당 플러그인을 사용하여 바코드 스캐너 기능을 구현하고자 할 때 호환성 문제를 고려해야합니다.

## 호환성 정보

### Flutter 버전과의 호환성

현재 `flutter_barcode_scanner` 플러그인은 Flutter 2.0 이상에서 사용 가능합니다. Flutter 2.0 이전 버전에서는 호환되지 않을 수 있으므로 주의가 필요합니다.

### iOS 버전과의 호환성

`flutter_barcode_scanner` 플러그인은 iOS 11 이상의 버전에서 작동합니다. 이전 버전의 iOS에서는 호환되지 않을 수 있으므로, 최신 버전의 iOS로 업데이트하는 것이 좋습니다.

### Android 버전과의 호환성

Android 앱에서 `flutter_barcode_scanner` 플러그인을 사용하려면 Android 4.1 이상의 버전이 필요합니다. 따라서 낮은 버전의 Android를 타겟팅하는 경우에는 호환성 문제가 발생할 수 있으므로 주의가 필요합니다.

## 결론

`flutter_barcode_scanner` 플러그인은 Flutter 2.0 이상, iOS 11 이상, Android 4.1 이상의 버전과 호환됩니다. 이러한 호환성 정보에 따라 개발 환경과 타겟 플랫폼의 버전을 고려하여 플러그인을 사용해야합니다. 추가적인 호환성 문제가 발생하는 경우에는 해당 플러그인의 공식 문서 및 소스 코드를 참조하는 것이 좋습니다.

## 참고 자료

- `flutter_barcode_scanner` 플러그인 GitHub 페이지: [https://github.com/mrtgumus/flutter_barcode_scanner](https://github.com/mrtgumus/flutter_barcode_scanner)