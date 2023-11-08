---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 드래그 핸들러 커스터마이징하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

`flutter_reorderable_list`는 플러터 애플리케이션에서 아이템을 재정렬할 수 있는 리스트 위젯입니다. 이 라이브러리를 사용하면 사용자가 아이템을 드래그하여 순서를 변경할 수 있습니다.

아이템 드래그 핸들러는 기본적으로 아이템 위젯의 왼쪽에 나타나지만, 때로는 이 핸들러의 모양을 변경하거나 추가 기능을 구현해야 할 수도 있습니다. 이번 블로그 포스트에서는 `flutter_reorderable_list`에서 아이템 드래그 핸들러를 커스터마이징하는 방법을 알아보겠습니다.

## 1. 드래그 핸들러 위젯 생성하기

드래그 핸들러를 커스터마이징하려면 먼저 드래그 핸들러 위젯을 생성해야 합니다. 이 위젯은 `GestureDetector`를 사용하여 터치 이벤트를 처리하고 드래그 동작에 대응해야 합니다.

```dart
import 'package:flutter/material.dart';

class CustomDragHandle extends StatelessWidget {
  final Widget child;

  const CustomDragHandle({Key key, this.child}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onPanStart: (details) {
        // 드래그 시작 시 동작 구현
      },
      onPanUpdate: (details) {
        // 드래그 중인 동안의 동작 구현
      },
      onPanEnd: (details) {
        // 드래그 종료 시 동작 구현
      },
      child: child,
    );
  }
}
```

위 코드에서 `CustomDragHandle`은 `GestureDetector`를 사용하여 터치 이벤트를 처리하는 위젯입니다. `onPanStart`, `onPanUpdate`, `onPanEnd` 콜백 함수를 사용하여 드래그 시작, 드래그 중, 드래그 종료 시 동작을 구현할 수 있습니다.

## 2. ReorderableListView와 함께 사용하기

이제 위에서 생성한 `CustomDragHandle` 위젯을 `ReorderableListView`와 함께 사용해보겠습니다. `ReorderableListView`는 아이템들을 재정렬할 수 있는 리스트 위젯입니다.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';

class CustomReorderableList extends StatefulWidget {
  @override
  _CustomReorderableListState createState() => _CustomReorderableListState();
}

class _CustomReorderableListState extends State<CustomReorderableList> {
  List<String> _items = ['Item 1', 'Item 2', 'Item 3', 'Item 4'];

  @override
  Widget build(BuildContext context) {
    return ReorderableListView(
      children: _items.map((item) {
        return ReorderableListItem(
          key: ValueKey(item),
          childBuilder: (BuildContext context, ReorderableItemState state) {
            return ListTile(
              key: ValueKey(item),
              title: Text(item),
              leading: CustomDragHandle(
                child: Icon(Icons.drag_handle),
              ),
            );
          },
        );
      }).toList(),
      onReorder: (oldIndex, newIndex) {
        setState(() {
          if (newIndex > oldIndex) {
            newIndex -= 1;
          }
          var item = _items.removeAt(oldIndex);
          _items.insert(newIndex, item);
        });
      },
    );
  }
}
```

위 코드에서는 `_items` 리스트의 각 아이템을 `ReorderableListItem`으로 나타내고, `CustomDragHandle`을 아이템 왼쪽에 배치하고 있습니다. `onReorder` 콜백 함수를 사용하여 아이템의 순서를 변경할 수 있습니다.

## 3. 커스터마이징된 드래그 핸들러 사용하기

이제 `CustomReorderableList` 위젯을 애플리케이션에서 사용해 보세요. 드래그 핸들러를 커스터마이징하여 아이콘 대신 이미지를 사용하거나, 추가 동작을 구현하는 등 원하는 방식으로 사용할 수 있습니다.

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Reorderable List Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Reorderable List Demo'),
        ),
        body: CustomReorderableList(),
      ),
    );
  }
}
```

위 코드는 애플리케이션을 실행하여 `ReorderableListView`와 함께 `CustomDragHandle`을 사용하는 예제입니다.

이렇게 `flutter_reorderable_list`에서 아이템 드래그 핸들러를 커스터마이징하는 방법을 알아보았습니다. 원하는 스타일과 동작을 구현하여 사용자가 아이템을 편리하게 재정렬할 수 있도록 만들어보세요.

## 참고 자료
- [flutter_reorderable_list 라이브러리 문서](https://pub.dev/packages/flutter_reorderable_list)
- [Flutter 공식 문서](https://flutter.dev/)