---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 투명도 조절하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

안녕하세요! 이번에는 Flutter 앱에서 아이템의 투명도를 조절하는 방법에 대해 알아보겠습니다. 특히, flutter_reorderable_list 패키지를 사용하여 아이템을 드래그하여 재정렬할 수 있는 경우에 대해 다루겠습니다.

## flutter_reorderable_list란?

flutter_reorderable_list는 Flutter 앱에서 아이템을 재정렬하기 위한 패키지입니다. 이 패키지를 사용하면 간단한 코드로 드래그 앤 드롭으로 아이템을 재정렬할 수 있습니다.

## 아이템 투명도 조절

flutter_reorderable_list에서 아이템의 투명도를 조절하려면 아이템 위젯의 opacity 속성을 변경해야 합니다. 다음은 예시 코드입니다.

```dart
ReorderableListView(
  children: List.generate(
    itemCount,
    (index) {
      return Opacity(
        opacity: getItemOpacity(index), // 아이템 투명도를 반환하는 함수 호출
        child: YourItemWidget(),
      );
    },
  ),
  // ...
);
```

위의 코드에서 `getItemOpacity` 함수는 해당 인덱스에 해당하는 아이템의 투명도를 반환하는 함수입니다. 이 함수를 사용하여 특정 조건에 따라 아이템의 투명도를 동적으로 조절할 수 있습니다.

이제 `getItemOpacity` 함수를 작성해보겠습니다.

```dart
double getItemOpacity(int index) {
  // 여기에서 특정 조건에 따라 아이템의 투명도를 계산합니다.
  // 예를 들어, 인덱스가 홀수일 때는 0.5의 투명도를 반환하고,
  // 짝수일 때는 1.0의 투명도를 반환할 수 있습니다.

  if (index % 2 == 0) {
    return 1.0;
  } else {
    return 0.5;
  }
}
```

위의 예시 코드에서는 인덱스가 홀수일 때는 투명도 0.5로 설정하고, 짝수일 때는 투명도 1.0으로 설정하도록 구현되어 있습니다. 여러분은 이 함수를 원하는 대로 수정하여 특정 조건에 따라 아이템의 투명도를 조절할 수 있습니다.

이렇게 하면 flutter_reorderable_list에서 아이템의 투명도를 조절할 수 있습니다. 원하는 조건에 따라 투명도를 동적으로 변경하여 애니메이션 효과를 줄 수도 있습니다.