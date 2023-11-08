---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 애니메이션 추가하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

## 소개
`flutter_reorderable_list`는 Flutter에서 재배치 가능한(reorderable) 리스트를 구현하는 데 사용되는 플러그인입니다. 이 플러그인은 사용자가 리스트의 아이템을 드래그하여 순서를 변경할 수 있도록 해주는 기능을 제공합니다. 그러나 기본적으로 아이템간의 애니메이션 효과는 제공되지 않기 때문에, 이를 추가하고 싶다면 별도의 작업이 필요합니다.

## 애니메이션 추가 방법
`flutter_reorderable_list`에서 아이템 애니메이션을 추가하기 위해서는 아래 단계를 따르면 됩니다.

### 단계 1: 애니메이션 컨트롤러 생성
```dart
AnimationController _animationController;
```
첫 번째 단계는 애니메이션 컨트롤러를 생성하는 것입니다. 이 컨트롤러는 아이템 애니메이션을 제어하는 데 사용됩니다.

### 단계 2: 애니메이션 컨트롤러 초기화
```dart
@override
void initState() {
  super.initState();
  
  _animationController = AnimationController(
    duration: const Duration(milliseconds: 200),
    vsync: this,
  );
}
```
리스트를 구성하는 위젯의 `initState` 메서드 내에서 애니메이션 컨트롤러를 초기화합니다. 애니메이션의 지속 시간과 vsync를 설정해야 합니다.

### 단계 3: 아이템 위젯에 애니메이션 적용
```dart
@override
Widget build(BuildContext context) {
  return ReorderableList(
    onReorder: (int oldIndex, int newIndex) {
      // 리스트 아이템 순서 변경 로직
    },
    children: <Widget>[
      for (int index = 0; index < items.length; index++)
        ReorderableItem(
          key: Key('$index'),
          childBuilder: (BuildContext context, ReorderableItemState state) {
            return SizeTransition(
              axis: Axis.vertical,
              sizeFactor: _animationController.drive(
                CurveTween(curve: Curves.easeInOut),
              ),
              child: // 아이템 위젯
            );
          },
        ),
    ],
  );
}
```
위 코드에서 주목해야 할 부분은 `childBuilder` 함수 내에서 `SizeTransition` 위젯을 사용하여 아이템 애니메이션을 적용한 부분입니다. 이 때, `SizeTransition` 위젯은 `_animationController.drive()` 메서드를 통해 애니메이션 컨트롤러를 연결하여 사용합니다. 

## 결론
`flutter_reorderable_list`에서 아이템 애니메이션을 추가하는 방법에 대해 알아보았습니다. 위의 단계를 따라 진행하면 사용자가 아이템 순서를 변경할 때 아이템 간의 부드러운 애니메이션 효과를 적용할 수 있습니다. 이를 통해 더욱 사용자 친화적인 재배치 가능한 리스트를 구현할 수 있습니다.

## 참고 자료
- [flutter_reorderable_list 플러그인](https://pub.dev/packages/flutter_reorderable_list)