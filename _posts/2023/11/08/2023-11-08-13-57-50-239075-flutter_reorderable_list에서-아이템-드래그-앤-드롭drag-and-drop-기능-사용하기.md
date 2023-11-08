---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 드래그 앤 드롭(Drag and Drop) 기능 사용하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

## 개요

Flutter는 대단히 유연하고 다양한 위젯들을 제공합니다. 이러한 위젯들 중에서 flutter_reorderable_list는 리스트의 아이템을 드래그 앤 드롭하여 재정렬할 수 있는 기능을 제공합니다. 

이번 글에서는 flutter_reorderable_list를 사용하여 아이템 드래그 앤 드롭 기능을 구현하는 방법에 대해 알아보겠습니다.

## flutter_reorderable_list란?

flutter_reorderable_list는 ReorderableListView 위젯을 사용하여 리스트의 아이템을 드래그 앤 드롭하여 재정렬할 수 있는 기능을 제공하는 패키지입니다. 

## 설치

먼저 `pubspec.yaml` 파일의 `dependencies` 섹션에 다음과 같이 flutter_reorderable_list를 추가합니다.

```yaml
dependencies:
  flutter_reorderable_list: ^0.2.2
```

그리고 패키지를 설치하기 위해 터미널에서 다음 명령어를 실행합니다.

```
flutter packages get
```

## 사용 방법

### 1. 패키지 import

먼저, 아래와 같이 flutter_reorderable_list 패키지를 import 해줍니다.

```dart
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';
```

### 2. 리스트 생성

리스트를 생성하기 위해 `ReorderableList` 위젯을 사용합니다. 

```dart
ReorderableList(
  onReorder: (oldIndex, newIndex) {
    setState(() {
      // 아이템 재정렬 로직 구현
    });
  },
  child: ListView.builder(
    itemCount: itemList.length,
    itemBuilder: (context, index) {
      return _buildItem(itemList[index], index);
    },
  ),
),
```

`onReorder` 콜백 함수는 아이템이 재정렬될 때마다 호출되는 함수입니다. 이 함수에서 아이템 재정렬에 대한 로직을 구현해야 합니다.

### 3. 아이템 위젯 생성

아이템 위젯을 생성하기 위해 `_buildItem` 메서드를 작성합니다.

```dart
Widget _buildItem(String item, int index) {
  return ListTile(
    key: Key('$item-$index'),
    title: Text(item),
    // 추가적인 위젯 속성들
  );
}
```

각 아이템은 `ListTile` 위젯으로 구성되며, `key` 속성을 통해 아이템을 식별합니다.

## 마무리

flutter_reorderable_list를 사용하면 쉽게 아이템 드래그 앤 드롭 기능을 구현할 수 있습니다. 이 패키지를 사용하여 사용자의 편의성을 높일 수 있는 앱을 개발해 보세요.

더 자세한 내용은 [flutter_reorderable_list GitHub 페이지](https://github.com/hanshengchiu/flutter_reorderable_list)를 참고하시기 바랍니다.