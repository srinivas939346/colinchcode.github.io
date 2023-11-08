---
layout: post
title: "[flutter] flutter_reorderable_list로 아이템 업데이트하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

이번 포스트에서는 Flutter 앱에서 아이템을 재배열하고 업데이트하는 방법을 알아보겠습니다. 이를 위해서 `flutter_reorderable_list` 패키지를 사용할 것입니다. 이 패키지는 리스트 항목을 드래그 앤 드롭으로 재배열할 수 있는 기능을 제공합니다.

## 패키지 설치

먼저, `flutter_reorderable_list` 패키지를 설치해야 합니다. `pubspec.yaml` 파일에 다음과 같이 패키지를 추가해주세요:

```yaml
dependencies:
  flutter_reorderable_list: ^0.2.0
```

그리고 패키지를 가져와서 사용할 수 있도록 `main.dart` 파일에 import 문을 추가해주세요:

```dart
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';
```

## FlutterReorderableList 생성

아이템을 재배열할 수 있는 리스트를 생성하기 위해 `FlutterReorderableList` 위젯을 사용합니다. 이 위젯 안에는 `itemBuilder`와 `onReorder` 콜백을 제공해야 합니다.

```dart
FlutterReorderableList(
  itemBuilder: (BuildContext context, int index) {
    // 각 아이템 별 UI 생성
    return ListTile(
      key: Key('$index'), // 위젯에 고유한 키를 부여해야 합니다
      title: Text('Item $index'),
    );
  },
  
  onReorder: (int oldIndex, int newIndex) {
    // 아이템 재배열 시 호출되는 콜백
    // oldIndex: 이전 위치, newIndex: 새로운 위치
    // 아이템을 업데이트하는 작업을 수행합니다
    // 예를 들어, 아이템의 순서를 업데이트한다던지, 데이터를 저장한다던지 할 수 있습니다
  },
);
```

## 아이템 업데이트

아이템을 업데이트하는 방법은 `onReorder` 콜백에서 수행됩니다. `oldIndex`와 `newIndex` 매개변수를 사용하여 이전 위치와 새로운 위치를 알 수 있습니다.

```dart
onReorder: (int oldIndex, int newIndex) {
  // 기존 아이템 리스트를 저장하고, 아이템을 재배열합니다
  List<Item> savedList = List<Item>.from(items);
  Item item = savedList.removeAt(oldIndex);
  savedList.insert(newIndex, item);

  // 업데이트된 아이템 리스트를 적용합니다
  setState(() {
    items = savedList;
  });
},
```

위의 코드에서 `items`는 리스트의 아이템을 저장하는 변수입니다. `oldIndex`로 현재 위치의 아이템을 가져오고, 이를 `savedList`에서 삭제한 후 `newIndex`에 해당하는 위치에 다시 삽입합니다. 그리고 `setState()`를 호출하여 UI를 업데이트합니다.

## 마무리

위의 단계를 따라가면 Flutter 앱에서 아이템을 재배열하고 업데이트하는 기능을 구현할 수 있습니다. `flutter_reorderable_list` 패키지의 다양한 기능을 활용하여 사용자가 원하는 대로 UI와 데이터를 업데이트할 수 있습니다.

더 많은 정보를 찾고 싶다면, `flutter_reorderable_list` 패키지의 [공식 문서](https://pub.dev/packages/flutter_reorderable_list)를 참고해주세요.