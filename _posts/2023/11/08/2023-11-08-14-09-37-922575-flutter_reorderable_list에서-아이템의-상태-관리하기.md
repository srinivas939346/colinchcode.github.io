---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템의 상태 관리하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

[flutter_reorderable_list](https://pub.dev/packages/flutter_reorderable_list)는 플러터에서 항목의 순서를 변경할 수 있는 목록 위젯이다. 이 위젯은 Drag & Drop 작업을 사용하여 항목을 재정렬할 수 있도록 도와준다. 

하지만 가끔은 항목의 상태를 함께 관리해야 할 때도 있다. 예를 들어, 특정 항목이 선택되었는지 여부를 추적하거나, 항목의 배경색을 변경하거나, 항목의 체크 상태를 확인해야 할 수 있다. 이런 상황에서는 항목의 상태를 관리할 수 있는 방법이 필요하다.

## Reorderable 항목의 상태 관리하기

`flutter_reorderable_list`의 각 항목은 `Reorderable` 위젯으로 래핑될 수 있다. 이를 통해 항목의 상태를 관리할 수 있다.

```dart
Reorderable(
  key: Key(item.id),
  builder: (BuildContext context, ReorderableItemState state) {
    // 항목을 빌드하는 로직

    return Container(
      // 항목 위젯의 디자인 및 내용
    ),
  },
)
```

위의 예시에서 `Reorderable` 위젯은 `key` 속성을 통해 각 항목의 고유한 식별자를 가지게 된다. 이를 사용하여 항목의 상태를 관리할 수 있다. 다음으로, 항목의 빌더 함수에서는 `ReorderableItemState` 파라미터를 통해 항목의 현재 상태를 받아올 수 있다.

## 항목 선택 상태 관리하기

항목을 선택 상태와 비선택 상태로 구분하여 관리해야 한다면, 각 항목에 대한 선택 여부를 저장하는 `isSelected` 변수를 만들어 사용할 수 있다.

```dart
class ListItem {
  final String id;
  bool isSelected;

  ListItem(this.id, {this.isSelected = false});
}
```

`isSelected` 변수는 `ListItem` 클래스에 추가되며, 기본값은 `false`로 설정된다.

이제 선택 상태를 변경하기 위한 콜백 함수를 항목 위젯에 전달하고, 해당 콜백 함수를 호출하여 `isSelected` 값을 변경할 수 있다.

```dart
Reorderable(
  key: Key(item.id),
  builder: (BuildContext context, ReorderableItemState state) {
    return InkWell(
      onTap: () {
        setState(() {
          item.isSelected = !item.isSelected;
        });
      },
      child: Container(
        // 항목 위젯의 디자인 및 내용
        color: item.isSelected ? Colors.blue : Colors.white,
      ),
    );
  },
)
```

위의 예시에서는 `InkWell` 위젯을 사용하여 항목을 터치할 때마다 선택 상태를 토글한다. 이때 `setState` 함수를 호출하여 상태 변경을 알려주어야 한다.

## 항목 체크 상태 관리하기

항목의 체크 상태를 관리하기 위해서는, `isChecked` 변수를 `ListItem` 클래스에 추가하여 사용할 수 있다.

```dart
class ListItem {
  final String id;
  bool isSelected;
  bool isChecked;

  ListItem(this.id, {this.isSelected = false, this.isChecked = false});
}
```

`isChecked` 변수는 해당 항목이 체크되었는지 여부를 저장한다.

체크박스를 표시하는 위젯을 항목에 추가하고, 체크 상태를 변경하는 콜백 함수를 정의한다.

```dart
Reorderable(
  key: Key(item.id),
  builder: (BuildContext context, ReorderableItemState state) {
    return InkWell(
      onTap: () {
        setState(() {
          item.isSelected = !item.isSelected;
        });
      },
      child: Container(
        // 항목 위젯의 디자인 및 내용
        color: item.isSelected ? Colors.blue : Colors.white,
        child: Checkbox(
          value: item.isChecked,
          onChanged: (value) {
            setState(() {
              item.isChecked = value;
            });
          },
        ),
      ),
    );
  },
)
```

위의 예시에서는 `Checkbox` 위젯을 사용하여 항목의 체크 상태를 표시하고, `onChanged` 콜백 함수를 통해 체크 상태 변경을 처리한다.

이제 `isChecked` 변수를 사용하여 항목의 체크 상태를 관리할 수 있다.

---

flutter_reorderable_list에서 항목의 상태를 관리하는 방법에 대해 알아보았다. 항목 선택 여부나 체크 상태와 같은 상태를 관리할 때는 각 항목에 대한 변수를 사용하여 상태를 저장하고, 상태를 변경하는 콜백 함수를 작성하여 업데이트해야 한다. 이를 통해 플러터 앱에서 `flutter_reorderable_list`를 활용할 때 더욱 유연하게 상태를 관리할 수 있다.