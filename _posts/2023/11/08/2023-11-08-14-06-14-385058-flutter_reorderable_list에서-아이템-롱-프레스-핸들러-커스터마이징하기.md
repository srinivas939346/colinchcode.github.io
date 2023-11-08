---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 롱 프레스 핸들러 커스터마이징하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

flutter_reorderable_list는 Flutter에서 사용할 수 있는 라이브러리로, 리스트 아이템의 순서를 바꿀 수 있는 기능을 제공합니다. 이 라이브러리를 사용하면 사용자는 리스트의 아이템을 드래그하여 재정렬 할 수 있습니다. 하지만 기본적으로 제공되는 롱 프레스 핸들러는 사용자에게 제한된 기능을 제공합니다. 이번 블로그 포스트에서는 flutter_reorderable_list의 아이템 롱 프레스 핸들러를 커스터마이징하는 방법에 대해 알아보겠습니다.

## 1. flutter_reorderable_list 설치하기

먼저, flutter_reorderable_list를 설치해야 합니다. 아래의 명령어를 사용하여 의존성을 추가해주세요.

```dart
dependencies:
  flutter_reorderable_list: ^0.2.0
```

의존성을 추가한 후 `flutter pub get` 명령어를 사용하여 패키지를 설치해주세요.

## 2. 아이템 롱 프레스 핸들러 커스터마이징하기

아이템 롱 프레스 핸들러를 커스터마이징하기 위해서는 `ReorderableList` 위젯을 사용해야 합니다. `ReorderableList` 위젯의 `itemBuilder` 콜백 메서드에서 아이템 위젯을 생성하고, `onReorder` 콜백 메서드에서 아이템의 순서를 업데이트 할 수 있습니다.

먼저, `ReorderableList`를 사용해 리스트를 생성해보겠습니다.

```dart
ReorderableList(
  onReorder: (int oldIndex, int newIndex) {
    // 아이템의 순서를 업데이트하는 로직을 구현합니다.
  },
  itemBuilder: (BuildContext context, int index) {
    // 아이템 위젯을 생성하는 로직을 구현합니다.
    return ListTile(
      key: Key("$index"),
      title: Text("Item $index"),
    );
  },
),
```

`itemBuilder` 메서드 안에서 `ListTile` 위젯을 반환하는 예시입니다. 이제 아이템을 롱 프레스하면 기본으로 제공되는 핸들러가 활성화됩니다. 이 기본 핸들러를 커스터마이징하기 위해서는 `ReorderableItem` 위젯을 사용해야 합니다.

```dart
itemBuilder: (BuildContext context, int index) {
  return ReorderableItem(
    key: Key("$index"),
    childBuilder: (BuildContext context, ReorderableItemState state) {
      // 아이템 위젯을 생성하는 로직을 구현합니다.
      return ListTile(
        key: Key("$index"),
        title: Text("Item $index"),
      );
    },
  );
},
```

`ReorderableItem` 위젯은 `childBuilder` 콜백 메서드를 가지고 있는데, 이곳에서 실제 아이템 위젯을 생성할 수 있습니다. `ReorderableItemState` 인자를 사용하여 아이템의 현재 상태를 확인할 수 있습니다.

아이템 롱 프레스 핸들러를 커스터마이징하기 위해서는 `childBuilder` 안에서 `LongPressGestureRecognizer`를 사용하여 원하는 동작을 구현해야 합니다.

```dart
itemBuilder: (BuildContext context, int index) {
  return ReorderableItem(
    key: Key("$index"),
    childBuilder: (BuildContext context, ReorderableItemState state) {
      return GestureDetector(
        onLongPress: () {
          // 롱 프레스 이벤트 핸들러를 구현합니다.
        },
        child: ListTile(
          key: Key("$index"),
          title: Text("Item $index"),
        ),
      );
    },
  );
},
```

위 예시에서는 `onLongPress` 이벤트 핸들러를 구현해야 합니다. 여기에 필요한 동작을 추가하여 아이템 롱 프레스 핸들러를 커스터마이징 할 수 있습니다.

## 마무리

flutter_reorderable_list에서 아이템 롱 프레스 핸들러를 커스터마이징하는 방법에 대해 알아보았습니다. 기본적인 라이브러리를 사용하지 않고 개발자가 직접 커스텀한 핸들러를 구현하여 사용자 경험을 개선할 수 있습니다. 더 많은 기능을 활용하여 앱을 개발해보세요!

참고: [flutter_reorderable_list](https://pub.dev/packages/flutter_reorderable_list)