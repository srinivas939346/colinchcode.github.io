---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 드래그 중 이벤트 처리하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

`flutter_reorderable_list`는 플러터에서 아이템의 순서를 변경할 수 있는 재정렬 가능한 리스트를 구현할 수 있는 패키지입니다. 이 패키지를 사용하면 사용자는 리스트의 아이템을 드래그하여 순서를 변경할 수 있게 됩니다.

하지만 때때로, 사용자가 아이템을 드래그하는 중에 다른 이벤트를 처리해야 할 수도 있습니다. 이 글에서는 `flutter_reorderable_list`에서 아이템 드래그 중에 이벤트를 처리하는 방법에 대해 알아보겠습니다.

## 드래그 이벤트 감지하기

`flutter_reorderable_list`에서 아이템 드래그 이벤트를 감지하는 방법은 `ReorderableDragStartListener`와 `ReorderableDragEndListener` 위젯을 사용하는 것입니다.

```dart
ReorderableList(
  ...
  onReorder: (oldIndex, newIndex) {
    // 아이템 재정렬 시 처리할 작업
  },
  child: ReorderableDragStartListener(
    index: index,
    child: ReorderableDragEndListener(
      index: index,
      child: ListTile(
        ...
      ),
    ),
  ),
);
```

위 코드에서 `ReorderableDragStartListener`는 아이템이 드래그 시작될 때 호출되는 동작을 정의할 수 있습니다. 마찬가지로, `ReorderableDragEndListener`는 아이템 드래그 종료 시 호출될 동작을 정의할 수 있습니다.

## 아이템 드래그 중에 이벤트 처리하기

아이템이 드래그 중일 때 추가적인 이벤트를 처리하려면 `ReorderableListener` 위젯을 사용해야 합니다.

```dart
ReorderableListener(
  // 이벤트 처리를 위해 이 위젯 사용
  child: ListTile(
    ...
  ),
)
```

위 코드에서 `ReorderableListener`는 아이템이 드래그되는 동안 추가 이벤트를 처리할 수 있도록 해줍니다. 이 위젯을 사용하면, 아이템의 드래그 중인 위치에 따라 적절한 동작을 수행할 수 있습니다.

## 예시

아래 예시는 `flutter_reorderable_list`에서 아이템을 드래그하는 동안 아이템의 배경색을 변경하는 방법을 보여줍니다.

```dart
ReorderableList(
  ...
  child: ReorderableDragStartListener(
    index: index,
    child: ReorderableDragEndListener(
      index: index,
      child: ReorderableListener(
        child: ListTile(
          tileColor: isDragging ? Colors.red : Colors.blue, // 드래그 중일 때 배경색 변경
          ...
        ),
      ),
    ),
  ),
);
```

위 코드에서 `isDragging` 변수는 아이템이 드래그되는 동안 `true`로 설정되고, 드래그 종료 시에는 `false`로 설정됩니다. 이를 통해 아이템의 배경색을 드래그 중인지에 따라 변경할 수 있습니다.

## 결론

`flutter_reorderable_list`에서 아이템 드래그 중에 이벤트를 처리하는 방법을 배웠습니다. `ReorderableDragStartListener`, `ReorderableDragEndListener`, 그리고 `ReorderableListener`를 사용하여 원하는 동작을 구현할 수 있습니다. 이를 통해 플러터 앱에서 사용자 친화적인 재정렬 가능한 리스트를 구현할 수 있게 됩니다.

더 자세한 정보나 예제는 [flutter_reorderable_list GitHub 페이지](https://github.com/fluttercommunity/flutter_reorderable_list)를 참조하십시오.