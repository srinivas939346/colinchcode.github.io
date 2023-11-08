---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 텍스트 스타일링하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

`flutter_reorderable_list`는 플러터에서 아이템을 재정렬하는 기능을 제공하는 패키지입니다. 이 패키지를 사용하면 사용자가 목록의 아이템 순서를 변경할 수 있습니다. 이번에는 `flutter_reorderable_list`를 사용하여 아이템의 텍스트 스타일링하는 방법에 대해 알아보겠습니다.

아이템의 텍스트 스타일을 변경하려면 먼저 `ReorderableListView` 위젯을 사용하여 목록을 만들어야 합니다. 아래는 간단한 예제 코드입니다.

```dart
ReorderableListView(
  children: <Widget>[
    ListTile(
      key: ValueKey(1),
      title: Text("아이템 1"),
      subtitle: Text("부제목 1"),
    ),
    ListTile(
      key: ValueKey(2),
      title: Text("아이템 2"),
      subtitle: Text("부제목 2"),
    ),
    ListTile(
      key: ValueKey(3),
      title: Text("아이템 3"),
      subtitle: Text("부제목 3"),
    ),
  ],
  onReorder: (int oldIndex, int newIndex) {
    // 아이템을 재정렬하는 로직 작성
  },
)
```

이제 아이템의 텍스트 스타일링을 변경해보겠습니다. `ListTile` 위젯에서 `title` 및 `subtitle` 속성을 사용하여 텍스트를 설정할 수 있습니다. 이 속성들은 `Text` 위젯을 받으므로 `Text` 위젯의 `style` 속성을 사용하여 텍스트 스타일을 지정할 수 있습니다.

예를 들어, 아이템의 제목을 빨간색과 볼드체로 설정하고 싶다면 다음과 같이 코드를 수정할 수 있습니다.

```dart
ListTile(
  key: ValueKey(1),
  title: Text(
    "아이템 1",
    style: TextStyle(
      color: Colors.red,
      fontWeight: FontWeight.bold,
    ),
  ),
  subtitle: Text("부제목 1"),
),
```

위와 같은 방식으로 `TextStyle`를 사용하여 원하는 텍스트 스타일을 설정할 수 있습니다. 추가적으로 `Text` 위젯의 다른 속성들을 활용하여 텍스트를 커스터마이즈할 수도 있습니다.

`flutter_reorderable_list`에서 아이템 텍스트를 스타일링하는 방법에 대해 알아보았습니다. 이제 원하는대로 아이템의 텍스트를 디자인할 수 있습니다.