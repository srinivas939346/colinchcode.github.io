---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 선택 해제하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

`flutter_reorderable_list`는 플러터(Flutter) 앱에서 아이템을 재정렬하는 기능을 제공하는 패키지입니다. 이 패키지를 사용하면 사용자가 아이템을 드래그하여 순서를 변경할 수 있습니다. 하지만, 기본적으로는 아이템을 선택한 상태로 유지하는데, 아이템 선택을 해제하는 방법에 대해 알아보겠습니다.

## 1. `ReorderableListView` 위젯 사용하기

먼저, `flutter_reorderable_list` 패키지에서 제공하는 `ReorderableListView` 위젯을 사용하여 재정렬 가능한 리스트를 만듭니다. 다음은 간단한 예시 코드입니다.

```dart
ReorderableListView(
  onReorder: (oldIndex, newIndex) {
    // 아이템 재정렬 로직
  },
  children: [
    for (var item in itemList)
      ListTile(
        key: Key(item.id),
        title: Text(item.title),
        onTap: () {
          // 아이템 선택 로직
        },
      ),
  ],
)
```

위 코드에서 `onTap` 콜백 함수를 사용하여 아이템을 선택할 수 있습니다.

## 2. 아이템 선택 해제하기

`flutter_reorderable_list`에서 아이템을 선택 해제하는 방법은 간단합니다. `ReorderableListView` 위젯의 `children`으로 전달하는 `ListTile` 위젯의 `onTap` 콜백 함수에서 아이템 선택 상태를 변경하면 됩니다. 다음은 선택 해제하는 방법을 보여주는 예시 코드입니다.

```dart
ReorderableListView(
  onReorder: (oldIndex, newIndex) {
    // 아이템 재정렬 로직
  },
  children: [
    for (var item in itemList)
      ListTile(
        key: Key(item.id),
        title: Text(item.title),
        onTap: () {
          setState(() {
            item.isSelected = !item.isSelected; // 아이템 선택 상태 변경
          });
        },
        tileColor: item.isSelected ? Colors.grey : null, // 선택 상태에 따라 타일 색상 변경
      ),
  ],
)
```

위 코드에서 `itemList`은 `List` 형태의 아이템 목록이며, 각 아이템은 선택 여부를 나타내는 `isSelected` 속성을 가지고 있습니다. `onTap` 콜백 함수에서 `isSelected` 속성을 토글하여 선택 상태를 변경하고, `tileColor` 속성을 사용하여 선택된 아이템의 타일 색상을 변경합니다.

이제 위 코드를 실행하면 사용자가 아이템을 선택하거나 해제할 수 있습니다.

위에서 설명한 방법을 사용하여 `flutter_reorderable_list`에서 아이템 선택 해제를 구현할 수 있습니다. 필요에 따라 코드를 수정하여 자신의 앱에 적용해보세요.

참고 자료:
- `flutter_reorderable_list` 패키지: [https://pub.dev/packages/flutter_reorderable_list](https://pub.dev/packages/flutter_reorderable_list)