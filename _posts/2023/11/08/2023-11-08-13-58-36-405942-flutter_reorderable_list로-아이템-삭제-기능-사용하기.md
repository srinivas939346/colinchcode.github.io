---
layout: post
title: "[flutter] flutter_reorderable_list로 아이템 삭제 기능 사용하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

`flutter_reorderable_list` 패키지는 플러터 앱에서 아이템을 재정렬할 수 있는 기능을 제공합니다. 이 기능을 이용하여 아이템을 삭제하는 방법에 대해 알아보겠습니다.

## 패키지 설치

`flutter_reorderable_list` 패키지를 사용하기 위해 `pubspec.yaml` 파일에 의존성을 추가해야 합니다. 다음과 같이 `pubspec.yaml` 파일을 수정해주세요:

```yaml
dependencies:
  flutter_reorderable_list: ^0.2.2
```

수정 후에는 패키지를 다운로드하고 아이디어를 업데이트하기 위해 `flutter pub get` 명령을 실행해야 합니다.

## 아이템 삭제 기능 추가하기

아이템 삭제 기능을 추가하려면 `ReorderableListView` 위젯을 사용해야 합니다. `ReorderableListView`는 `children` 속성을 통해 재정렬 가능한 아이템의 목록을 받습니다. 아래 코드는 `ReorderableListView` 위젯을 사용하여 아이템 삭제 기능을 구현한 예시입니다:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';

class MyItemList extends StatefulWidget {
  @override
  _MyItemListState createState() => _MyItemListState();
}

class _MyItemListState extends State<MyItemList> {
  List<String> _items = [
    'Item 1',
    'Item 2',
    'Item 3',
    'Item 4',
    'Item 5',
  ];

  @override
  Widget build(BuildContext context) {
    return ReorderableListView(
      onReorder: (int oldIndex, int newIndex) {
        setState(() {
          if (newIndex > oldIndex) {
            newIndex -= 1;
          }
          final item = _items.removeAt(oldIndex);
          _items.insert(newIndex, item);
        });
      },
      children: _items.map((item) {
        final key = Key(item);
        return Dismissible(
          key: key,
          child: ListTile(
            key: key,
            title: Text(item),
          ),
          onDismissed: (direction) {
            setState(() {
              _items.remove(item);
            });
          },
          background: Container(
            color: Colors.red,
            child: Icon(Icons.delete),
            alignment: Alignment.centerRight,
          ),
        );
      }).toList(),
    );
  }
}

```

위의 코드에서는 `ReorderableListView`로 아이템 목록을 표시하고, `Dismissible` 위젯을 추가하여 아이템을 삭제할 수 있는 기능을 제공합니다. `Dismissible` 위젯은 슬라이드하여 삭제하는 동작을 지원하며, `onDismissed` 콜백을 사용하여 삭제된 아이템을 상태에서 제거합니다.

이제 `MyItemList` 위젯을 사용하여 삭제 가능한 아이템 목록을 만들 수 있습니다.

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('My App'),
        ),
        body: MyItemList(),
      ),
    );
  }
}
```

## 결론

`flutter_reorderable_list` 패키지를 사용하여 플러터 앱에서 아이템 삭제 기능을 구현할 수 있습니다. 위의 예시 코드를 참고하여 개발하시면 됩니다.