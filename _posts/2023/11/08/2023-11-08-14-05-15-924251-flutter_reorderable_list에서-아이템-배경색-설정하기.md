---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 배경색 설정하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

안녕하세요! Flutter 개발자 여러분들을 위한 팁을 소개해드립니다. 오늘은 `flutter_reorderable_list` 패키지를 사용하여 아이템의 배경색을 설정하는 방법에 대해 알아보겠습니다.

`flutter_reorderable_list`는 사용자가 목록 항목의 순서를 변경할 수 있도록 도와주는 패키지입니다. 여기에는 아이템들을 드래그하여 재정렬할 수 있는 기능이 포함되어 있습니다. 

이러한 패키지를 사용하면 아이템의 배경색을 사용자의 요구에 맞게 변경할 수 있습니다. 

## 패키지 설치하기

먼저, `flutter_reorderable_list` 패키지를 사용하기 위해서는 `pubspec.yaml` 파일에 해당 패키지를 추가해주어야 합니다. 아래의 코드를 `pubspec.yaml`의 `dependencies` 섹션에 추가해주세요.

```yaml
dependencies:
  flutter_reorderable_list: ^0.2.5
```

패키지를 추가한 후에는 `flutter packages get` 명령어를 사용하여 패키지를 설치해주세요.

## 아이템 배경색 설정하기

`flutter_reorderable_list`에서 아이템의 배경색을 설정하려면 `ReorderableList` 위젯 내에서 `ReorderableItem` 위젯을 사용해야 합니다. `ReorderableItem` 위젯은 `child` 속성을 통해 각 아이템의 내용을 정의할 수 있습니다.

```dart
ReorderableList(
  itemBuilder: (BuildContext context, int index) {
    return ReorderableItem(
      key: Key('$index'),
      childBuilder: (BuildContext context, ReorderableItemState state) {
        return Container(
          color: state.isHighlighted ? Colors.blue : Colors.transparent,
          child: ListTile(
            title: Text('Item $index'),
          ),
        );
      },
    );
  },
  itemCount: 10,
  onReorder: (int oldIndex, int newIndex) {
    // 재정렬 이벤트 처리
  },
)
```

위의 코드에서 `ReorderableItem`의 `childBuilder` 콜백 함수에서 `Container` 위젯의 `color` 속성을 설정하여 아이템의 배경색을 결정할 수 있습니다. `state.isHighlighted`를 사용하여 현재 아이템이 드래그되어 있는지 여부를 확인할 수 있습니다. 드래그 중인 아이템은 `Colors.blue`로 배경색을 설정하고, 나머지 아이템은 `Colors.transparent`로 배경색을 설정하도록 예시로 작성하였습니다.

## 결론

`flutter_reorderable_list` 패키지를 사용하여 아이템의 배경색을 설정하는 방법을 알아보았습니다. 이를 통해 사용자가 목록 항목의 순서를 쉽게 변경할 수 있는 기능을 구현하고, 디자인 요구사항에 맞게 아이템의 배경색을 변경할 수 있습니다. 

기타 다른 기능들에 대해서는 [공식 문서](https://pub.dev/packages/flutter_reorderable_list)를 참고하시기 바랍니다.