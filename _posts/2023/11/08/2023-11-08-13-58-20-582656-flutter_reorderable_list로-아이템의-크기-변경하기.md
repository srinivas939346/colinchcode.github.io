---
layout: post
title: "[flutter] flutter_reorderable_list로 아이템의 크기 변경하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

## 소개

flutter_reorderable_list 패키지는 플러터 앱에서 아이템의 순서를 바꿀 수 있게 해주는 강력한 기능을 제공합니다. 그러나 기본적으로 모든 아이템은 동일한 크기를 가지고 있습니다. 이번 블로그 포스트에서는 flutter_reorderable_list를 사용하여 아이템의 크기를 변경하는 방법을 알려드리겠습니다.

## 방법

1. 먼저, flutter_reorderable_list 패키지를 프로젝트에 추가해야 합니다. `pubspec.yaml` 파일에 다음과 같이 의존성을 추가하세요.

```yaml
dependencies:
  flutter_reorderable_list: ^0.3.0
```

2. 이제 `main.dart` 파일에서 패키지를 가져옵니다.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';
```

3. flutter_reorderable_list를 사용하여 아이템의 크기를 변경하려면 `ReorderableList` 위젯 내에서 `ItemReorderable` 위젯을 사용해야 합니다. 다음은 기본적인 코드 예시입니다.

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: ReorderableList(
          onReorder: (int oldIndex, int newIndex) {
            // 리스트 아이템을 재정렬할 때 호출되는 콜백 함수
          },
          child: ListView.builder(
            itemBuilder: (BuildContext context, int index) {
              return ItemReorderable(
                // 아이템 위젯
              );
            },
            itemCount: 10, // 리스트의 아이템 개수
          ),
        ),
      ),
    );
  }
}
```

4. `ItemReorderable` 위젯 내에서 원하는 아이템 크기를 설정할 수 있습니다. 예를 들어, 컨테이너의 높이를 조절하려면 `height` 속성을 사용합니다. 아래는 코드 예시입니다.

```dart
ItemReorderable(
  key: UniqueKey(),
  height: 100, // 아이템의 높이를 100으로 설정
  childBuilder: (BuildContext context, ReorderableItemState state) {
    return Container(
      height: 100, // 아이템이 들어갈 컨테이너의 높이를 100으로 설정
      child: // 아이템의 내용
    );
  },
);
```

5. 마지막으로, `onReorder` 콜백 함수를 사용하여 아이템을 재정렬할 때마다 크기가 변경되도록 설정할 수 있습니다.

```dart
ReorderableList(
  // ...
  onReorder: (int oldIndex, int newIndex) {
    // 리스트 아이템을 재정렬할 때 호출되는 콜백 함수
    // 아이템의 크기를 변경하는 로직을 추가하세요
  },
  // ...
);
```

## 결론

flutter_reorderable_list를 사용하여 아이템의 크기를 변경하는 방법을 알아보았습니다. 이를 통해 플러터 앱에서 더 유연하고 다양한 아이템 레이아웃을 구현할 수 있습니다. 좀 더 자세한 내용은 공식 문서를 참고하세요.

> [flutter_reorderable_list 패키지](https://pub.dev/packages/flutter_reorderable_list)