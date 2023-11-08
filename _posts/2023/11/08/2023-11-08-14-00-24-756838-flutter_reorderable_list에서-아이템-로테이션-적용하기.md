---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 로테이션 적용하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

**플러터 (Flutter)**는 Google에서 개발한 사용자 인터페이스(UI)를 구축하기 위한 오픈소스 프레임워크입니다. 신속하고 효율적인 개발을 위해 많은 개발자들이 플러터를 선택하고 있습니다. 이번 블로그 포스트에서는 **flutter_reorderable_list** 패키지를 사용하여 아이템 로테이션을 적용하는 방법을 알아보겠습니다.

## flutter_reorderable_list란?

**flutter_reorderable_list**는 플러터에서 리스트 아이템을 재정렬할 수 있는 기능을 제공하는 패키지입니다. 사용자가 리스트 아이템을 드래그하여 순서를 변경할 수 있게 됩니다.

## 아이템 로테이션 적용하기

### 패키지 추가하기

먼저, **flutter_reorderable_list** 패키지를 프로젝트에 추가해야 합니다. `pubspec.yaml` 파일의 `dependencies` 섹션에 다음과 같이 패키지를 추가합니다:

```yaml
dependencies:
  flutter_reorderable_list: ^0.2.2
```

### 아이템 위젯 만들기

로테이션을 적용할 아이템을 위한 위젯을 만듭니다. 이 예제에서는 단순한 컨테이너 위젯을 사용하도록 하겠습니다:

```dart
Widget buildItem(BuildContext context, int index, bool isActive) {
  return Container(
    key: ValueKey(index),
    height: 100,
    color: isActive ? Colors.blue : Colors.grey,
    child: Center(
      child: Text('Item $index'),
    ),
  );
}
```

### ReorderableWidget 사용하기

위에서 만든 아이템 위젯을 ReorderableWidget에 담아 사용해야 합니다. ReorderableWidget은 **flutter_reorderable_list** 패키지에서 제공합니다. 다음과 같이 사용할 수 있습니다:

```dart
ReorderableWidget(
  onReorder: (oldIndex, newIndex) {
    // 아이템의 순서가 변경되었을 때 호출되는 콜백 함수
    // 순서 변경에 대한 로직을 구현해야 합니다
  },
  child: ListView.builder(
    itemCount: itemCount,
    itemBuilder: (context, index) {
      return buildItem(context, index, isActive);
    },
  ),
);
```

### 로테이션 로직 구현하기

순서 변경에 대한 로직은 `onReorder` 콜백 함수에서 구현해주어야 합니다. 이 함수는 아이템의 순서가 변경되었을 때 호출되며, 현재 위치와 새로운 위치를 인자로 받습니다. 아래는 예시 코드입니다:

```dart
onReorder: (oldIndex, newIndex) {
  setState(() {
    if (oldIndex < newIndex) {
      newIndex -= 1;
    }
    final item = items.removeAt(oldIndex);
    items.insert(newIndex, item);
  });
},
```

위 예시 코드에서는 `items`라는 콜렉션에서 아이템을 제거한 뒤, 새로운 위치에 아이템을 삽입하고 있습니다. 순서를 변경하는 방식은 프로젝트의 요구에 따라 다를 수 있으므로, 이 예시 코드를 필요에 맞게 수정하십시오.

## 결론

위의 단계를 따라가면 **flutter_reorderable_list** 패키지를 사용하여 플러터 앱에서 아이템 로테이션을 적용할 수 있습니다. 이를 통해 사용자들은 리스트 아이템 순서를 쉽게 재정렬할 수 있게 됩니다. 자세한 내용은 [flutter_reorderable_list GitHub 페이지](https://github.com/hanshengchiu/flutter_reorderable_list)에서 확인할 수 있습니다.