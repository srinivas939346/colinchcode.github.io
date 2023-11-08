---
layout: post
title: "[flutter] flutter_reorderable_list로 아이템 드롭 효과 주기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

![Flutter Logo](https://flutter.dev/images/flutter-logo-sharing.png)

## 개요
앱 개발시 아이템의 순서를 변경하고 싶을 때, 아이템을 드래그하여 재정렬하는 기능은 매우 유용합니다. 이러한 드롭 효과를 주기 위해서는 `flutter_reorderable_list` 패키지를 사용할 수 있습니다. 이 패키지는 Flutter 앱에서 아이템을 드래그하여 재정렬하는 기능을 제공합니다.

## 설치
`flutter_reorderable_list` 패키지를 사용하기 위해서는 먼저 `pubspec.yaml` 파일에 의존성을 추가해야 합니다. 아래와 같이 `flutter_reorderable_list` 패키지를 추가합니다.

```yaml
dependencies:
  flutter_reorderable_list: ^0.2.0
```

그리고 나서 `pub get` 명령어를 실행하여 패키지를 설치합니다.

## 사용 방법

아래의 예제 코드를 참고하여 `flutter_reorderable_list` 패키지를 사용하는 방법을 확인해보세요.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Reorderable List Example',
      home: ReorderableListExample(),
    );
  }
}

class ReorderableListExample extends StatefulWidget {
  @override
  _ReorderableListExampleState createState() => _ReorderableListExampleState();
}

class _ReorderableListExampleState extends State<ReorderableListExample> {
  List<String> itemList = [
    "Item 1",
    "Item 2",
    "Item 3",
    "Item 4",
    "Item 5"
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Reorderable List Example'),
      ),
      body: ReorderableListView(
        onReorder: (int oldIndex, int newIndex) {
          setState(() {
            if (newIndex > oldIndex) {
              newIndex -= 1;
            }
            final item = itemList.removeAt(oldIndex);
            itemList.insert(newIndex, item);
          });
        },
        children: itemList.map((item) {
          final key = Key('item_${itemList.indexOf(item)}');
          return ListTile(
            key: key,
            title: Text(item),
          );
        }).toList(),
      ),
    );
  }
}
```

위의 코드에서 주목할 부분은 `ReorderableListView` 위젯입니다. 이 위젯은 `onReorder` 콜백 함수를 설정하여 아이템을 재정렬할 수 있도록 합니다.

## 결론
`flutter_reorderable_list` 패키지를 사용하면 Flutter 앱에서 아이템의 드롭 효과를 주어 재정렬할 수 있습니다. 이러한 기능은 앱의 사용자 경험을 향상시키고 유저가 편리하게 아이템을 정리할 수 있는 기능을 제공합니다.

## 참고 자료
- [flutter_reorderable_list 패키지](https://pub.dev/packages/flutter_reorderable_list)
- [Flutter 공식 홈페이지](https://flutter.dev/)