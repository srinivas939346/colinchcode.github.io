---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 선택하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

flutter_reorderable_list는 아이템을 재정렬할 수 있는 플러터 (Flutter) 패키지입니다. 하지만 기본적으로는 아이템을 선택할 수 있는 기능은 제공되지 않습니다. 만약 flutter_reorderable_list에서 아이템을 선택하고 싶다면 어떻게 해야 할까요? 이 글에서는 그 방법에 대해 설명하겠습니다.

## 1. 아이템 선택 상태 관리하기

먼저, 아이템을 선택할 때 선택된 상태를 관리해야 합니다. 이를 위해 선택된 아이템의 인덱스 목록과 선택 상태를 저장할 수 있는 리스트를 사용합니다. 선택된 아이템의 인덱스 목록을 저장할 `List<int>` 변수와 선택 상태를 저장할 `List<bool>` 변수를 선언합니다.

```dart
List<int> selectedIndexList = [];
List<bool> isSelectedList = [];
```

## 2. 아이템 위젯에 선택 기능 추가하기

다음으로, 아이템 위젯에 선택 기능을 추가해야 합니다. 아이템 위젯은 `ReorderableItem` 위젯으로 표현됩니다. 각 아이템 위젯에 `onTap` 콜백을 추가하여 아이템을 클릭할 때마다 선택 상태를 업데이트합니다.

```dart
ReorderableItem(
  key: ValueKey(item.id),
  childBuilder: (BuildContext context, ReorderableItemState state) {
    return GestureDetector(
      onTap: () {
        setState(() {
          bool isSelected = !isSelectedList[itemIndex];
          isSelectedList[itemIndex] = isSelected;
          if (isSelected) {
            selectedIndexList.add(itemIndex);
          } else {
            selectedIndexList.remove(itemIndex);
          }
        });
      },
      child: Container(
        // 아이템 위젯의 내용
      ),
    );
  },
);
```

위 코드에서 `itemIndex`는 아이템의 인덱스 값을 의미합니다. 클릭할 때마다 선택 상태를 반전시키고, 선택된 아이템의 인덱스를 `selectedIndexList`에 추가하거나 제거합니다.

## 3. 선택된 아이템 처리하기

마지막으로, 선택된 아이템을 처리합니다. 예를 들어, 선택된 아이템을 다른 화면으로 넘겨줄 때 사용할 수 있습니다. `selectedIndexList`를 다른 화면으로 전달하거나 선택된 아이템의 데이터를 활용하는 방법은 여러 가지가 있습니다.

```dart
// 예시: 선택된 아이템 목록 출력
void printSelectedItems() {
  print(selectedIndexList.map((index) => itemList[index]).toList());
}
```

위 코드에서 `itemList`는 전체 아이템 목록을 의미합니다. 선택된 아이템 목록을 콘솔에 출력하는 `printSelectedItems` 메서드를 정의하였습니다.

## 마무리

이제 flutter_reorderable_list에서 아이템을 선택하는 방법에 대해 알게 되었습니다. `selectedIndexList`와 `isSelectedList` 변수를 사용하여 아이템 선택 상태를 관리하고, 그에 따라 선택 기능을 추가하고 선택된 아이템을 처리할 수 있습니다. 이를 활용하여 개인 프로젝트나 팀 프로젝트에서 더욱 유연하고 편리한 사용자 경험을 제공할 수 있습니다.

## 참고 자료

- [flutter_reorderable_list 패키지 문서](https://pub.dev/packages/flutter_reorderable_list)
- [플러터 (Flutter) 공식 사이트](https://flutter.dev/)