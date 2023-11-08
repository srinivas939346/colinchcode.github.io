---
layout: post
title: "[flutter] flutter_reorderable_list로 아이템 축소하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

이번 글에서는 Flutter 패키지인 `flutter_reorderable_list`를 사용하여 아이템을 축소하는 방법에 대해 알아보겠습니다.

## `flutter_reorderable_list`란?

`flutter_reorderable_list`는 Flutter에서 리스트 아이템의 순서를 변경하고 재정렬하는 기능을 제공하는 패키지입니다. 이 패키지는 사용자가 리스트 아이템을 드래그하여 다른 위치로 이동하거나, 아이템을 삭제하거나 추가하는 등의 작업을 할 수 있게 해줍니다.

## 아이템 축소하기

`flutter_reorderable_list`로 아이템을 축소하기 위해서는 아이템 위젯을 손쉽게 크기를 조절할 수 있도록 해야 합니다. 이를 위해 아이템 위젯은 `ReorderableDelayedDragHandle` 위젯으로 감싸야 합니다. 그리고 아이템의 크기를 조절하는 기능을 구현해야 합니다.

다음은 `flutter_reorderable_list`를 사용하여 아이템을 축소하는 예제 코드입니다.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';

class ReorderableListItem extends StatelessWidget {
  final Key key;
  final double itemWidth;
  final double itemHeight;
  final Widget content;

  ReorderableListItem({
    required this.key,
    required this.itemWidth,
    required this.itemHeight,
    required this.content,
  });

  @override
  Widget build(BuildContext context) {
    return SizedBox(
      key: key,
      width: itemWidth,
      height: itemHeight,
      child: ReorderableDelayedDragHandle(
        child: Card(
          child: content,
        ),
      ),
    );
  }
}

class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  List<Widget> items = [
    ReorderableListItem(
      key: UniqueKey(),
      itemWidth: 200.0,
      itemHeight: 100.0,
      content: Container(
        child: Text('Item 1'),
      ),
    ),
    ReorderableListItem(
      key: UniqueKey(),
      itemWidth: 200.0,
      itemHeight: 100.0,
      content: Container(
        child: Text('Item 2'),
      ),
    ),
    ReorderableListItem(
      key: UniqueKey(),
      itemWidth: 200.0,
      itemHeight: 100.0,
      content: Container(
        child: Text('Item 3'),
      ),
    ),
  ];

  @override
  Widget build(BuildContext context) {
    return ReorderableList(
      onReorder: (int oldIndex, int newIndex) {
        setState(() {
          Widget item = items.removeAt(oldIndex);
          items.insert(newIndex, item);
        });
      },
      child: ListView(
        children: items,
      ),
    );
  }
}
```

위 예제 코드에서는 `ReorderableListItem` 위젯을 사용하여 리스트 아이템을 생성합니다. 이 위젯은 `ReorderableDelayedDragHandle` 위젯으로 감싸져 있으며, `itemWidth`와 `itemHeight`를 이용하여 아이템의 크기를 조절합니다. 이렇게 구현된 아이템 위젯들을 `ReorderableList`에서 사용하여 재정렬 가능한 리스트를 생성합니다.

## 결론

`flutter_reorderable_list`를 사용하여 Flutter 앱에서 아이템을 축소하는 방법을 알아보았습니다. 이를 통해 사용자가 리스트 아이템을 쉽게 드래그 및 재정렬할 수 있게 됩니다. 이 패키지를 활용하여 사용자 친화적인 인터페이스를 구현해보세요!

## 참고 자료

- [flutter_reorderable_list](https://pub.dev/packages/flutter_reorderable_list) 패키지
- [Flutter - ReorderableList](https://flutter.dev/docs/cookbook/gestures/reorderable-list) Flutter Cookbook