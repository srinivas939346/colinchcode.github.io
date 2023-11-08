---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 배경 이미지 추가하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

[flutter_reorderable_list](https://pub.dev/packages/flutter_reorderable_list)은 플러터에서 아이템의 순서를 바꿀 수 있는 위젯입니다. 

이 위젯을 사용하여 아이템 목록을 만들 때, 각 아이템에 배경 이미지를 추가하고 싶은 경우가 있을 수 있습니다. 이런 경우 아래의 방법을 사용하여 flutter_reorderable_list에 아이템 배경 이미지를 추가할 수 있습니다.

## 1. 아이템 위젯 생성하기

먼저, 각 아이템을 위한 위젯을 생성합니다. 각 아이템 위젯은 `ReorderableItem` 위젯으로 감싸져야 합니다.

```dart
Widget buildItem(BuildContext context, int index) {
  return ReorderableItem(
    key: Key('$index'),
    childBuilder: (BuildContext context, ReorderableItemState state) {
      return Container(
        height: 100,
        decoration: BoxDecoration(
          image: DecorationImage(
            image: AssetImage('assets/item_background.png'),
            fit: BoxFit.cover,
          ),
        ),
        child: ListTile(
          title: Text('Item $index'),
        ),
      );
    },
  );
}
```

위의 코드에서 `Container` 위젯의 `decoration` 속성 안에 `image` 속성을 사용하여 배경 이미지를 설정합니다. `AssetImage` 클래스를 사용하여 이미지를 가져올 수 있습니다. `fit` 속성을 사용하여 이미지의 맞춤 방법을 설정할 수 있습니다.

## 2. 아이템 위젯 사용하기

`buildItem` 함수를 사용하여 아이템 위젯을 만들었다면, 이제 `ReorderableList` 위젯을 사용하여 아이템 목록을 생성합니다.

```dart
ReorderableList(
  onReorder: (oldIndex, newIndex) {},
  child: ListView.builder(
    itemCount: items.length,
    itemBuilder: (BuildContext context, int index) {
      return buildItem(context, index);
    },
  ),
)
```

위의 코드에서 `ReorderableList` 위젯의 `child` 속성에 `ListView.builder`를 사용하여 아이템 목록을 생성합니다. `itemBuilder` 함수에서 `buildItem` 함수를 호출하여 각 아이템 위젯을 생성합니다.

## 3. 결과 확인하기

이제 앱을 실행하여 아이템 목록에 배경 이미지가 추가되었는지 확인해보세요.

위의 방법을 따라하면 flutter_reorderable_list에서 아이템에 배경 이미지를 쉽게 추가할 수 있습니다.