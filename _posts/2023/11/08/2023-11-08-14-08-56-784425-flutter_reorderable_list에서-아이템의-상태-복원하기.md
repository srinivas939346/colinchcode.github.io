---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템의 상태 복원하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

## 개요
`flutter_reorderable_list`는 `Flutter`에서 리스트 아이템을 재정렬할 수 있는 기능을 제공하는 패키지입니다. 이 패키지를 사용하면 사용자가 드래그하여 아이템을 이동시킬 수 있으며, 아이템의 위치를 변경할 때마다 콜백 함수가 호출됩니다. 그러나 아이템의 상태를 유지하고 복원하는 기능은 기본적으로 제공되지 않습니다. 이번 글에서는 `flutter_reorderable_list`를 사용하여 아이템의 상태를 저장하고 복원하는 방법에 대해 살펴보겠습니다.

## 상태 저장하기

`flutter_reorderable_list`를 사용하여 아이템의 순서를 변경할 때마다 호출되는 콜백 함수는 사용자가 이동시킨 아이템의 새로운 위치와 이전 위치를 전달받습니다. 이 콜백 함수 내에서는 이동된 아이템의 상태를 저장할 수 있습니다. 대표적인 저장 방법은 `List`를 사용하는 것입니다. 

```dart
List<Item> itemList = [];
```

위와 같이 `Item` 클래스의 리스트를 생성하여 아이템을 저장합니다. `Item` 클래스는 이동 가능한 아이템에 대한 정보를 담고 있습니다. 해당 콜백 함수에서는 이동된 아이템의 위치를 찾아 이를 `itemList`에 저장합니다.

```dart
ReorderableList(
  // ... 생략 ...
  onReorder: (int oldIndex, int newIndex) {
    setState(() {
      // 이동된 아이템의 상태 저장
      Item movedItem = itemList.removeAt(oldIndex);
      itemList.insert(newIndex, movedItem);
    });
  },
)
```

이렇게 구현하면 아이템의 순서가 변경될 때마다 `itemList`에 이동된 아이템의 상태가 저장됩니다.

## 상태 복원하기

아이템의 상태를 복원하기 위해서는 저장된 상태를 가져와서 화면에 그려야 합니다. `flutter_reorderable_list`는 `itemBuilder` 파라미터를 통해 아이템을 그리는 위젯을 생성합니다. 이 때, `itemBuilder`에 전달되는 인덱스를 통해 `itemList`에서 해당 인덱스의 아이템을 가져와서 위젯을 그려줍니다.

```dart
ReorderableList(
  itemCount: itemList.length,
  itemBuilder: (BuildContext context, int index) {
    Item item = itemList[index];
    return MyItemWidget(item);
  },
)
```

따라서 상태를 복원하기 위해서는 앱 초기화 단계에서 `itemList`로부터 아이템을 가져와야 합니다. 이를 위해 앱의 초기화를 담당하는 `initState()` 메서드에서 저장된 상태를 불러와야 합니다.

```dart
@override
void initState() {
  super.initState();
  // 저장된 아이템 상태 복원
  itemList = loadItemList();
}

List<Item> loadItemList() {
  // 여기에서 저장된 아이템 상태를 불러온다.
  // 예: SharedPreferences, 파일 등을 사용하여 불러옴
  // ...
}

```

위와 같이 `loadItemList()` 메서드를 통해 저장된 아이템 상태를 불러올 수 있습니다. 이 때, 상태를 복원하는 방법은 저장할 때와 동일한 방법으로 아이템 리스트를 생성하는 것입니다.

## 결론
`flutter_reorderable_list`를 사용하여 아이템의 순서를 변경할 때, 아이템의 상태를 저장하고 복원하는 방법에 대해 알아보았습니다. 이를 통해 사용자가 아이템을 이동시키더라도 상태를 유지할 수 있게되며, 좀 더 사용자 친화적인 인터페이스를 구현할 수 있습니다.

자세한 내용은 [flutter_reorderable_list README](https://pub.dev/packages/flutter_reorderable_list)를 참고하시기 바랍니다.