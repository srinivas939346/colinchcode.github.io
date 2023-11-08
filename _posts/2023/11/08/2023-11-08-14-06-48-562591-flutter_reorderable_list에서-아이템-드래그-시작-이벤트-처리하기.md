---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 드래그 시작 이벤트 처리하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

# 개요
flutter_reorderable_list는 플러터(Flutter) 앱에서 아이템의 순서를 변경하고 재정렬할 수 있는 기능을 제공합니다. 이 라이브러리를 사용하면 사용자가 아이템을 드래그하여 위치를 변경할 수 있습니다. 이번 포스트에서는 flutter_reorderable_list에서 아이템 드래그 시작 이벤트를 처리하는 방법에 대해 알아보겠습니다.

# flutter_reorderable_list 설치
먼저 flutter_reorderable_list를 사용하기 위해 해당 라이브러리를 프로젝트에 추가해야 합니다. 아래의 명령을 실행하여 의존성을 추가할 수 있습니다.

```
dependencies:
  flutter_reorderable_list: ^0.2.1
```

의존성을 추가한 뒤에는 `flutter pub get` 명령을 실행하여 패키지를 다운로드합니다.

# 아이템 드래그 시작 이벤트 처리하기
flutter_reorderable_list는 `ReorderableList` 위젯과 `ReorderableItem` 위젯을 사용하여 아이템 드래그 및 재정렬 기능을 구현합니다. 아래의 코드는 `ReorderableList` 위젯과 `ReorderableItem` 위젯을 사용하여 아이템을 생성하는 예제입니다.

```dart
ReorderableList(
  onReorder: (oldIndex, newIndex) {
    // 아이템 재정렬 로직
  },
  child: ListView.builder(
    itemCount: itemList.length,
    itemBuilder: (context, index) {
      return ReorderableItem(
        key: Key('$index'),
        childBuilder: (context, state) {
          return ListTile(
            title: Text(itemList[index]),
          );
        },
      );
    },
  ),
)
```

위의 코드에서 `onReorder` 콜백 함수를 사용하여 아이템 재정렬 이벤트를 처리할 수 있습니다. 이 함수에서는 드래그 된 아이템의 이전 인덱스와 새로운 인덱스를 받아와서 아이템을 재정렬하는 로직을 작성하면 됩니다.

만약 아이템 드래그가 시작될 때 어떠한 작업을 처리하고 싶다면 `onDragStarted` 콜백 함수를 사용하면 됩니다. 이 함수는 다음과 같이 `ReorderableItem` 위젯의 `onDragStarted` 속성을 통해 설정할 수 있습니다.

```dart
ReorderableItem(
  key: Key('$index'),
  childBuilder: (context, state) {
    return ListTile(
      title: Text(itemList[index]),
    );
  },
  onDragStarted: () {
    // 아이템 드래그 시작 이벤트 처리
  },
)
```

이제 `onDragStarted` 콜백 함수에서 원하는 동작을 수행하면 됩니다. 예를 들어, 드래그가 시작되었을 때 아이템을 특정 색상으로 강조 표시하거나, 드래그 된 아이템의 정보를 출력하는 등의 작업을 할 수 있습니다.

# 마무리
이번 포스트에서는 flutter_reorderable_list에서 아이템 드래그 시작 이벤트를 처리하는 방법에 대해 알아보았습니다. 해당 기능을 사용하면 플러터 앱에서 아이템의 순서를 손쉽게 변경하고 재정렬할 수 있습니다. 현재 참고한 라이브러리 버전에 따라 API가 변경될 수 있으니, 사용하기 전에 공식 문서나 예제를 확인하는 것을 추천합니다.

# 참고 자료
- [flutter_reorderable_list 패키지](https://pub.dev/packages/flutter_reorderable_list)
- [flutter_reorderable_list 공식 문서](https://github.com/hanshengchiu/flutter_reorderable_list)