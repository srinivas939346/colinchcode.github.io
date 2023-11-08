---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 활성화 및 비활성화하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

`flutter_reorderable_list`는 Flutter 앱에서 아이템의 순서를 재정렬할 수 있는 기능을 제공합니다. 이 플러그인을 사용하여 리스트의 아이템을 활성화하거나 비활성화할 수 있는 방법을 알아보겠습니다.

## 1. flutter_reorderable_list 플러그인 추가하기

먼저, `pubspec.yaml` 파일에 `flutter_reorderable_list` 플러그인을 추가해야 합니다. 아래와 같이 `dependencies` 섹션에 플러그인을 추가합니다.

```yaml
dependencies:
  flutter_reorderable_list: ^2.1.0
```

플러그인을 추가한 후, 터미널에서 `flutter pub get` 명령어를 실행하여 의존성을 가져옵니다.

## 2. ReorderableListView 구성하기

`flutter_reorderable_list`의 핵심 요소는 `ReorderableListView`입니다. 아래와 같이 `ReorderableListView`를 구성하여 리스트를 생성합니다.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';

class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  List<String> items = ['Item 1', 'Item 2', 'Item 3'];

  @override
  Widget build(BuildContext context) {
    return ReorderableListView(
      onReorder: (int oldIndex, int newIndex) {
        setState(() {
          if (newIndex > oldIndex) newIndex -= 1;
          final String item = items.removeAt(oldIndex);
          items.insert(newIndex, item);
        });
      },
      children: List.generate(
        items.length,
        (index) {
          final item = items[index];

          return ListTile(
            key: Key('$index'),
            title: Text(item),
          );
        },
      ),
    );
  }
}
```

`ReorderableListView`는 `onReorder` 콜백을 제공하여 아이템의 순서가 변경될 때 수행할 동작을 정의합니다. 위의 예제에서는 `setState`를 호출하여 아이템의 순서를 변경하고 화면을 다시 그립니다.

## 3. 아이템 활성화 및 비활성화하기

`flutter_reorderable_list`에서는 아이템을 활성화하거나 비활성화하기 위해 `ReorderableListItem` 위젯과 `ReorderableListener` 위젯을 사용할 수 있습니다. 아래 예제에서는 각 아이템을 드래그하여 순서를 변경할 수 있도록 활성화하고, 일시적으로 순서 변경이 불가능한 상태일 때 비활성화합니다.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';

class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  List<String> items = ['Item 1', 'Item 2', 'Item 3'];
  bool isReorderingEnabled = true;

  @override
  Widget build(BuildContext context) {
    return ReorderableListView(
      onReorder: (int oldIndex, int newIndex) {
        setState(() {
          if (newIndex > oldIndex) newIndex -= 1;
          final String item = items.removeAt(oldIndex);
          items.insert(newIndex, item);
        });
      },
      children: List.generate(
        items.length,
        (index) {
          final item = items[index];

          return ReorderableListener(
            child: ListTile(
              key: Key('$index'),
              title: Text(item),
            ),
            isEnabled: isReorderingEnabled,
          );
        },
      ),
    );
  }
}
```

위의 예제에서는 `isReorderingEnabled`라는 불리언 변수를 사용하여 아이템의 활성화 상태를 변경할 수 있습니다. `ReorderableListener`의 `isEnabled` 속성을 이 변수와 연결하여 아이템을 활성화 또는 비활성화합니다.

## 결론

`flutter_reorderable_list`를 사용하면 Flutter 앱에서 아이템의 순서를 재정렬하는 기능을 쉽게 구현할 수 있습니다. 위의 예제를 참고하여 아이템을 활성화/비활성화하는 기능을 추가해 보세요.

---

## 참고 자료

- [flutter_reorderable_list 패키지](https://pub.dev/packages/flutter_reorderable_list)