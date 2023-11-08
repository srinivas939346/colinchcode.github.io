---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 라벨 추가하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

`flutter_reorderable_list`는 플러터(Flutter) 앱에서 아이템을 재정렬할 수 있는 리스트를 구현하는데 사용되는 패키지입니다. 이 패키지는 사용자가 아이템을 드래그앤드롭을 통해 순서를 변경할 수 있게 해주기 때문에 매우 유용하게 사용될 수 있습니다.

하지만 `flutter_reorderable_list`는 아이템의 라벨을 직접적으로 지원하지 않습니다. 따라서 이 기능을 추가하려면 몇 가지 추가 작업이 필요합니다.

## 1. 아이템 모델에 라벨 추가

`flutter_reorderable_list`에서 사용할 아이템 모델에 라벨을 추가해야 합니다. 예를 들어, 각 아이템에 문자열 라벨을 사용하려면 다음과 같이 모델을 수정합니다.

```dart
class ListItem {
  String label;
  // 나머지 프로퍼티...
}
```

## 2. 아이템 위젯 수정

다음으로, 아이템 위젯에서 라벨을 표시하는 위젯을 추가해야 합니다. 이 위젯은 `flutter_reorderable_list` 패키지의 `ReorderableItem` 위젯 내부에서 사용됩니다. 다음은 라벨을 표시하는 예제입니다.

```dart
class MyListItem extends StatelessWidget {
  final ListItem item;

  MyListItem(this.item);

  @override
  Widget build(BuildContext context) {
    return ReorderableItem(
      key: Key(item.id),
      childBuilder: (BuildContext context, ReorderableItemState state) {
        return Container(
          // 아이템 위젯 구성...
          child: Column(
            children: [
              Text(item.label, style: TextStyle(fontSize: 16)),
              // 기타 내용...
            ],
          ),
        );
      },
    );
  }
}
```

이제 각 아이템 위젯에 라벨이 표시됩니다.

## 3. 아이템 재정렬

기본적으로 `flutter_reorderable_list`는 아이템을 재정렬하는 기능을 제공합니다. 사용자가 아이템을 드래그앤드롭하여 순서를 변경할 수 있게 되는 것입니다.

## 참고 자료

- `flutter_reorderable_list` 패키지: https://pub.dev/packages/flutter_reorderable_list