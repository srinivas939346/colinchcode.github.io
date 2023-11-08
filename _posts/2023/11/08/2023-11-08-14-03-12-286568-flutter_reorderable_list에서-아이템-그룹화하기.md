---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 그룹화하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

`flutter_reorderable_list`는 Flutter에서 reorderable한 리스트를 구현할 수 있는 패키지입니다. 이 패키지를 사용하면 사용자가 목록의 아이템을 재정렬할 수 있습니다. 그러나 기본적으로는 단일 그룹으로 구성되어 있습니다.

이번에는 `flutter_reorderable_list`에서 아이템을 그룹화하여 사용하는 방법에 대해 알아보겠습니다.

## 그룹화된 아이템 사용하기

그룹화된 아이템을 사용하기 위해서는 `ReorderableGroupBuilder` 위젯을 추가하여 각 그룹을 정의해야 합니다. 이 위젯은 `ReorderableList` 위젯의 `children` 속성 대신에 사용됩니다.

```dart
ReorderableGroupBuilder(
  itemBuilder: (BuildContext context, int index) {
    // 아이템 위젯 생성
    return ReorderableItem();
  },
  itemCount: groupItemCount, // 전체 그룹의 아이템 개수
  groupId: groupId, // 그룹 아이디
)
```

위의 코드에서 `itemBuilder`는 각 아이템 위젯을 생성합니다. `itemCount`는 해당 그룹의 아이템 개수를 나타내며, `groupId`는 그룹을 식별하는 고유한 아이디입니다.

`ReorderableItem` 위젯은 각 아이템을 나타내며, `key` 속성을 사용하여 고유한 키 값을 할당해야 합니다.

```dart
ReorderableItem(
  key: ValueKey(uniqueId),
  childBuilder: (BuildContext context, ReorderableItemState state) {
    // 아이템 위젯 내용
    return Container();
  },
)
```

위의 코드에서 `key` 속성을 사용하여 각 아이템에 고유한 키 값을 할당합니다. `childBuilder`는 아이템 위젯의 내용을 생성합니다. 

## 그룹화된 아이템의 이동 처리하기

그룹화된 아이템을 이동할 때, `flutter_reorderable_list` 패키지는 기본적으로 아이템의 이동을 처리하지 않습니다. 따라서 우리가 직접 이동을 처리해야 합니다.

모든 그룹화된 아이템에 대한 이동 이벤트를 처리하려면, 각 `ReorderableGroupBuilder` 위젯에 `onReorder` 콜백을 추가해야 합니다.

```dart
ReorderableGroupBuilder(
  onReorder: (int oldIndex, int newIndex, bool isGroup) {
    // 아이템 이동 처리
  },
  // ...
)
```

위의 코드에서 `onReorder` 콜백은 아이템 이동 이벤트를 처리합니다. `oldIndex`는 이동되기 전의 인덱스를, `newIndex`는 이동된 후의 인덱스를 나타냅니다. `isGroup`은 이동 대상이 그룹인지 여부를 나타냅니다.

## 결론

`flutter_reorderable_list` 패키지를 사용하여 Flutter 앱에서 그룹화된 아이템을 구현하는 방법에 대해 알아보았습니다. `ReorderableGroupBuilder` 위젯을 사용하여 그룹을 정의하고, `onReorder` 콜백을 이용하여 아이템 이동을 처리할 수 있습니다.

더 자세한 내용은 [flutter_reorderable_list](https://pub.dev/packages/flutter_reorderable_list) 패키지의 공식 문서를 참조하시기 바랍니다.