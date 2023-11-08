---
layout: post
title: "[flutter] flutter_reorderable_list 라이브러리의 기능과 기능 설명"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

## 개요
flutter_reorderable_list 라이브러리는 Flutter 앱에서 리스트의 항목을 재정렬할 수 있는 기능을 제공하는 라이브러리입니다. 이 라이브러리를 사용하면 사용자가 끌어서 놓기 동작으로 항목의 순서를 변경할 수 있으며, 사용자 친화적인 인터페이스를 제공할 수 있습니다. 이 글에서는 flutter_reorderable_list 라이브러리의 주요 기능 및 사용법에 대해 자세히 알아보겠습니다.

## 기능 설명

### 리스트 항목 순서 변경
flutter_reorderable_list 라이브러리를 사용하면 리스트의 항목을 끌어서 놓기를 통해 순서를 변경할 수 있습니다. 사용자가 항목을 길게 누르고 드래그하면, 해당 항목이 다른 위치로 이동하게 됩니다. 이를 통해 사용자는 원하는 순서로 항목을 재배열할 수 있습니다. 

### 드래그 핸들 지원
라이브러리는 항목 별로 드래그 핸들을 지원합니다. 사용자가 드래그 핸들을 잡고 이동하면 해당 항목이 원하는 위치로 이동하게 됩니다. 드래그 핸들은 항목의 왼쪽, 오른쪽, 위, 아래 등 다양한 위치에 배치할 수 있습니다. 이를 통해 사용자는 편리하게 항목을 재배열할 수 있습니다.

### 애니메이션 지원
flutter_reorderable_list는 항목의 순서가 변경될 때 자연스러운 애니메이션 효과를 제공합니다. 항목이 새로운 위치로 이동할 때, 부드럽고 자연스러운 애니메이션을 통해 사용자 경험을 향상시킵니다. 이를 통해 앱의 사용성과 직관성을 높일 수 있습니다.

### 다양한 커스터마이징 옵션
flutter_reorderable_list는 다양한 커스터마이징 옵션을 제공합니다. 항목의 드래그 핸들 색상, 모양, 크기 등을 변경하거나, 순서 변경 애니메이션 속도를 조절하는 등의 설정이 가능합니다. 개발자는 앱의 디자인과 사용자 경험을 최적화하기 위해 이러한 옵션을 사용할 수 있습니다.

## 예제 코드

```dart
import 'package:flutter/material.dart';
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';

class MyReorderableList extends StatefulWidget {
  @override
  _MyReorderableListState createState() => _MyReorderableListState();
}

class _MyReorderableListState extends State<MyReorderableList> {
  List<String> items = [
    'Item 1',
    'Item 2',
    'Item 3',
    'Item 4',
    'Item 5',
  ];

  void _onReorder(int oldIndex, int newIndex) {
    setState(() {
      if (newIndex > oldIndex) {
        newIndex -= 1;
      }
      final item = items.removeAt(oldIndex);
      items.insert(newIndex, item);
    });
  }

  @override
  Widget build(BuildContext context) {
    return ReorderableList(
      onReorder: _onReorder,
      child: ListView(
        children: [
          for (final item in items)
            ListTile(
              key: Key(item),
              title: Text(item),
            ),
        ],
      ),
    );
  }
}
```

위의 예제 코드는 flutter_reorderable_list 라이브러리를 사용한 간단한 예제입니다. ReorderableList 위젯을 사용하여 리스트를 생성하고, 항목이 들어있는 ListView를 child로 전달합니다. onReorder 콜백 함수에서 순서가 변경될 때마다 상태를 업데이트하고, 리스트를 다시 빌드하여 화면에 반영합니다.

## 참고 자료
- [flutter_reorderable_list 라이브러리 GitHub 페이지](https://github.com/hanshengchiu/flutter_reorderable_list)
- [flutter_reorderable_list 라이브러리 예제](https://pub.dev/packages/flutter_reorderable_list/example)