---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템의 상태 초기화하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

flutter_reorderable_list는 Flutter에서 재정렬 가능한 목록을 만들어주는 패키지입니다. 이 패키지를 사용하면 사용자가 목록의 아이템을 드래그 앤 드롭하여 순서를 변경할 수 있습니다. 하지만 때로는 목록의 아이템이 초기 상태로 돌아가야 할 필요가 있을 수 있습니다. 이번 포스트에서는 flutter_reorderable_list에서 아이템의 상태를 초기화하는 방법에 대해 알아보겠습니다.

## 아이템의 상태 초기화하기

flutter_reorderable_list를 사용할 때, 아이템의 상태를 초기화하는 방법은 다음과 같습니다.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';

class ReorderableListExample extends StatefulWidget {
  @override
  _ReorderableListExampleState createState() => _ReorderableListExampleState();
}

class _ReorderableListExampleState extends State<ReorderableListExample> {
  List<String> _items = ['Item 1', 'Item 2', 'Item 3'];

  @override
  Widget build(BuildContext context) {
    return ReorderableListView(
      children: _items.map((item) {
        return ListTile(
          key: Key(item),
          title: Text(item),
        );
      }).toList(),
      onReorder: (oldIndex, newIndex) {
        setState(() {
          if (newIndex > oldIndex) {
            newIndex -= 1;
          }
          final item = _items.removeAt(oldIndex);
          _items.insert(newIndex, item);
        });
      },
    );
  }
}
```

위의 예제 코드에서는 `_ReorderableListExampleState` 클래스에 `_items`라는 문자열 목록을 정의합니다. 각 아이템은 `ReorderableListView`의 자식으로 `ListTile` 위젯으로 표시됩니다. 사용자가 아이템의 순서를 변경하면 `onReorder` 콜백 함수가 호출되고, `_items` 목록이 업데이트됩니다.

이제 만약, 사용자가 재정렬을 통해 아이템의 순서를 변경한 후 모든 아이템을 초기 상태로 돌려야 할 경우 아래의 코드를 `onReorder` 콜백 함수 내부에 추가하면 됩니다.

```dart
setState(() {
  // 이전에 원하는 초기 상태로 아이템을 업데이트합니다.
  _items = ['Item 1', 'Item 2', 'Item 3'];
});
```

위의 코드는 `_items` 목록을 원하는 초기 상태인 `['Item 1', 'Item 2', 'Item 3']`로 업데이트합니다. 이렇게 하면 사용자가 목록을 재정렬한 후에 아이템의 순서를 초기 상태로 돌릴 수 있습니다.

## 마무리

이번 포스트에서는 flutter_reorderable_list에서 아이템의 상태를 초기화하는 방법에 대해 알아보았습니다. 사용자가 목록의 아이템을 재정렬한 후에 초기 상태로 돌아가야 할 경우, `onReorder` 콜백 함수 내부에서 `_items` 목록을 원하는 초기 상태로 업데이트하면 됩니다. 이를 통해 flutter_reorderable_list를 더욱 유연하게 사용할 수 있습니다.

더 자세한 내용은 [flutter_reorderable_list 공식 문서](https://pub.dev/packages/flutter_reorderable_list)를 참조하시기 바랍니다.