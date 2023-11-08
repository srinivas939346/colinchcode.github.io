---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 축소 이벤트 처리하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

## 소개

Flutter는 효율적인 사용자 인터페이스를 빌드하기 위한 인기있는 프레임워크입니다. `flutter_reorderable_list`는 사용자가 순서를 변경할 수 있는 재정렬 가능한 목록을 만들기 위한 유용한 패키지입니다. 이 패키지를 사용하여 아이템의 크기를 축소하는 이벤트를 처리하는 방법을 알아보겠습니다.

## 아이템 축소 이벤트 처리하기

1. `flutter_reorderable_list` 패키지를 프로젝트에 추가합니다. `pubspec.yaml` 파일을 열고 `dependencies` 섹션에 다음을 추가합니다:

   ```
   dependencies:
     flutter_reorderable_list: ^0.2.0
   ```

2. 축소 가능한 아이템을 만드는 방법을 알아봅시다. `ReorderableItem` 위젯을 사용하여 아이템을 생성합니다. 이 위젯은 이벤트를 처리할 수 있도록 `onResize` 콜백 함수를 제공합니다.

   ```dart
   ReorderableItem(
     key: ValueKey(item.id),
     childBuilder: (context, state) {
       return Container(
         height: state.dimensions.height,
         child: // 아이템 위젯
       );
     },
     onResize: (resizeData) {
       // 아이템의 크기가 변경될 때 호출되는 콜백 함수
       // 여기에서 아이템을 축소하도록 구현할 수 있습니다.
     },
   )
   ```

3. `onResize` 콜백 함수에서 아이템을 축소하는 로직을 구현합니다. 예를 들어, `AnimatedContainer`를 사용하여 아이템의 높이를 표시하고 축소 애니메이션을 추가할 수 있습니다.

   ```dart
   onResize: (resizeData) {
     setState(() {
       final newHeight = // 축소할 크기 계산
       state.dimensions = state.dimensions.copyWith(height: newHeight);
     });
   }
   ```

4. 이제 사용자가 아이템을 드래그하여 순서를 변경하거나 축소할 수 있습니다. 이제 `flutter_reorderable_list` 패키지를 사용하여 아이템을 재정렬하는 방법을 알고 있으므로 프로젝트에 적용할 수 있습니다.

## 요약

`flutter_reorderable_list` 패키지를 사용하면 사용자가 순서를 변경할 수 있는 재정렬 가능한 목록을 쉽게 구현할 수 있습니다. 이 패키지를 사용하여 아이템의 크기를 축소하는 이벤트를 처리하는 방법을 알아보았습니다. 축소 가능한 아이템을 생성하고 `onResize` 콜백 함수에서 아이템을 축소하는 로직을 구현하는 방법을 알게 되었습니다. 이제 앱에 이 기능을 추가하여 사용자가 아이템의 크기를 조정할 수 있도록 만들 수 있습니다.

## 참고 자료
- [flutter_reorderable_list 패키지](https://pub.dev/packages/flutter_reorderable_list)