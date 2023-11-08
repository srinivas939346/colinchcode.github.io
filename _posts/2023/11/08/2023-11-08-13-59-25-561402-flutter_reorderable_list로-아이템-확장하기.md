---
layout: post
title: "[flutter] flutter_reorderable_list로 아이템 확장하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

`flutter_reorderable_list`는 Flutter에서 아이템을 재정렬할 수 있는 기능을 제공하는 패키지입니다. 이 패키지를 사용하면 사용자가 리스트의 아이템을 드래그하여 원하는 순서로 재정렬할 수 있습니다.

하지만 기본적으로 `flutter_reorderable_list`는 아이템을 단순히 드래그하여 재정렬하는 기능만을 제공합니다. 만약 아이템을 확장하여 추가적인 기능이나 정보를 보여주고 싶다면 어떻게 해야할까요? 이번 기사에서는 `flutter_reorderable_list`를 사용하여 아이템을 확장하는 방법에 대해 알아보겠습니다.

## 아이템 확장하기

`flutter_reorderable_list`에서 아이템을 확장하기 위해서는 `ReorderableSliverList`를 사용해야 합니다. 이 위젯은 `SliverList`와 같이 스크롤 가능한 리스트를 구성합니다. 아래는 `ReorderableSliverList`를 사용하여 아이템을 확장하는 예제 코드입니다.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';

class ExtendedItem extends StatefulWidget {
  final Widget child;
  
  ExtendedItem({Key key, this.child}) : super(key: key);
  
  @override
  _ExtendedItemState createState() => _ExtendedItemState();
}

class _ExtendedItemState extends State<ExtendedItem> {
  bool _expanded = false;
  
  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        ListTile(
          title: Text('Item'),
          subtitle: Text('Subtitle'),
          onTap: () {
            setState(() {
              _expanded = !_expanded;
            });
          },
        ),
        if (_expanded) widget.child,
      ],
    );
  }
}

class ExampleScreen extends StatelessWidget {
  final List<String> itemList = ['Item 1', 'Item 2', 'Item 3'];

  @override
  Widget build(BuildContext context) {
    return CustomScrollView(
      slivers: [
        ReorderableSliverList(
          delegate: ReorderableSliverChildBuilderDelegate(
            (BuildContext context, int index) {
              return ExtendedItem(
                child: Text('Additional Information'),
              );
            },
            childCount: itemList.length,
          ),
          onReorder: (int oldIndex, int newIndex) {
            // 리스트 아이템 재정렬 로직 구현
          },
        ),
      ],
    );
  }
}
```

위 코드에서 `ExtendedItem` 위젯은 `ListTile`을 포함하는 컬럼입니다. `ListTile` 클릭 시 `_expanded`의 상태를 토글하여 기능을 확장하고 접을 수 있습니다. 추가적인 정보를 보여주기 위한 위젯은 `_expanded` 값에 따라 조건부적으로 렌더링됩니다.

## 결론

`flutter_reorderable_list`를 사용하여 아이템을 확장하는 방법에 대해 알아보았습니다. 이렇게 확장된 아이템을 사용하면 사용자가 원하는 형태로 리스트를 재정렬할 수 있으며, 추가적인 정보나 기능을 제공할 수 있습니다. 사용자 경험을 향상시키기 위해 `flutter_reorderable_list`의 다양한 기능을 활용해보세요.

## 참고 자료
- [flutter_reorderable_list 패키지](https://pub.dev/packages/flutter_reorderable_list)