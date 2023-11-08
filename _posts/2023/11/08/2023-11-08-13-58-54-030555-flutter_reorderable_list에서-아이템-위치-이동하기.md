---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 위치 이동하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

## 개요
때로는 사용자가 리스트의 아이템을 재배열하고 싶을 때가 있습니다. Flutter에서 `flutter_reorderable_list` 라이브러리를 사용하면 아주 간단하게 아이템의 위치를 이동할 수 있습니다. 이 블로그 포스트에서는 `flutter_reorderable_list`를 사용하여 아이템 위치를 이동하는 방법에 대해 알아보겠습니다.

## flutter_reorderable_list 설치

먼저, `flutter_reorderable_list` 패키지를 설치해야 합니다. `pubspec.yaml` 파일에 다음과 같이 패키지를 추가합니다:

```yaml
dependencies:
  flutter_reorderable_list: ^0.1.2
```

그런 다음, 패키지를 가져올 수 있도록 import 문을 추가합니다:

```dart
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';
```

## 아이템 목록 생성

처음에는 아이템 목록을 생성해야 합니다.`ReorderableList` 위젯의 `childern` 속성에는 실제 아이템 위젯 목록을 나열해야 합니다. 예를 들어, 다음과 같이 아이템 목록을 생성할 수 있습니다:

```dart
List<Widget> items = [
  ListTile(title: Text("Item 1")),
  ListTile(title: Text("Item 2")),
  ListTile(title: Text("Item 3")),
  // 아이템을 추가하거나 제거할 수 있습니다.
];
```

## 아이템 위치 이동

`ReorderableList` 위젯의 `onReorder` 콜백을 사용하여 아이템의 위치를 이동합니다. 콜백 함수에서는 현재 인덱스와 새로운 인덱스를 받아올 수 있습니다. 이를 사용하여 아이템 목록에서 아이템의 위치를 이동시킬 수 있습니다. 예를 들어, 다음과 같이 `onReorder` 콜백을 정의할 수 있습니다:

```dart
void handleReorder(int oldIndex, int newIndex) {
  if (oldIndex < newIndex) {
    newIndex -= 1;
  }
  final item = items.removeAt(oldIndex);
  items.insert(newIndex, item);
}
```

## ReorderableList 위젯 사용

이제 `ReorderableList` 위젯을 사용하여 아이템 목록을 표시합니다. `ReorderableList` 위젯은 `ListTile`과 같은 아이템 위젯과 함께 사용됩니다. 예를 들어, 다음과 같이 `ReorderableList`를 사용할 수 있습니다:

```dart
ReorderableList(
  onReorder: handleReorder,
  child: ListView(
    children: items,
  ),
)
```

이제 위젯을 빌드하고 실행하면 목록의 아이템을 드래그하여 위치를 이동할 수 있습니다.

## 결론

`flutter_reorderable_list` 라이브러리를 사용하여 Flutter 앱에서 아이템 위치를 이동하는 방법을 살펴보았습니다. 이 기능을 사용하면 사용자가 직접 목록의 아이템을 재배열할 수 있습니다. 

더 자세한 내용을 보려면 [flutter_reorderable_list](https://pub.dev/packages/flutter_reorderable_list) 패키지의 문서를 참조하세요.