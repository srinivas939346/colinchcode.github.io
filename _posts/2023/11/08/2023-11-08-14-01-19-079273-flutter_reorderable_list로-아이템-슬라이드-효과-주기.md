---
layout: post
title: "[flutter] flutter_reorderable_list로 아이템 슬라이드 효과 주기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

안녕하세요! 이번에는 Flutter에서 `flutter_reorderable_list` 패키지를 사용하여 아이템 슬라이드 효과를 주는 방법에 대해 알아보겠습니다.

## flutter_reorderable_list란?

`flutter_reorderable_list` 패키지는 Flutter에서 리스트 항목의 순서를 변경하고 다시 정렬할 수 있는 기능을 제공하는 패키지입니다. 사용자는 항목을 드래그하여 이동시킬 수 있으며, 이 중요한 기능을 아이템 슬라이드 효과와 결합하여 더 흥미로운 사용자 경험을 제공할 수 있습니다.

## 패키지 설치

먼저, `pubspec.yaml` 파일에서 `flutter_reorderable_list` 패키지를 추가해야 합니다. 아래와 같이 `dependencies` 섹션에 패키지를 추가해주세요.

```yaml
dependencies:
  flutter_reorderable_list: ^0.3.0
```

그리고 패키지를 설치하기 위해 터미널에서 다음 명령어를 실행해주세요.

```
flutter pub get
```

## 아이템 슬라이드 효과 주기

다음은 `flutter_reorderable_list` 패키지를 사용하여 아이템 슬라이드 효과를 주는 간단한 예제입니다.

1. 먼저, `flutter_reorderable_list` 패키지를 import 해주세요.

```dart
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';
```

2. `ReorderableList` 위젯을 사용하여 아이템을 나열합니다.

```dart
ReorderableList(
    onReorder: (int oldIndex, int newIndex) {
        // 아이템 이동 로직 구현
    },
    child: ListView.builder(
        itemCount: itemCount,
        itemBuilder: (BuildContext context, int index) {
            return ReorderableItem(
                key: Key('$index'),
                childBuilder: (BuildContext context, ReorderableItemState state) {
                    return ListTile(
                        key: ObjectKey(index),
                        title: Text('Item $index'),
                        // 슬라이드 효과를 주고 싶은 위젯 추가
                    );
                },
            );
        },
    ),
)
```

3. `onReorder` 콜백 함수를 구현하여 아이템 이동 로직을 처리합니다.

```dart
onReorder(int oldIndex, int newIndex) {
  setState(() {
    // 아이템 이동 로직 구현
  });
}
```

다음으로, 슬라이드 효과를 주고 싶은 위젯을 추가합니다. 여기에서는 `Dismissible` 위젯을 사용하여 슬라이드 효과를 구현하였습니다.

4. `Dismissible` 위젯으로 아이템에 슬라이드 효과를 추가합니다.

```dart
childBuilder: (BuildContext context, ReorderableItemState state) {
    return Dismissible(
        key: ValueKey(index),
        direction: DismissDirection.horizontal,
        onDismissed: (direction) {
          // 아이템 삭제 로직 구현
        },
        background: Container(
          color: Colors.red,
          child: Icon(Icons.delete),
          alignment: Alignment.centerRight,
        ),
        child: ListTile(
            key: ObjectKey(index),
            title: Text('Item $index'),
        ),
    );
},
```

이제, 해당 아이템을 스와이프하면 빨간색 배경과 오른쪽에 "삭제" 아이콘이 나타납니다. 이 아이템을 스와이프하여 삭제할 수 있습니다.

## 결론

`flutter_reorderable_list` 패키지를 사용하면 쉽게 아이템 슬라이드 효과를 주고 사용자가 리스트 항목의 순서를 변경할 수 있는 기능을 구현할 수 있습니다. 이를 통해 더 흥미롭고 직관적인 사용자 경험을 제공할 수 있습니다. 참고로, 위 예제에서는 `Dismissible`를 사용하였지만, 다른 슬라이드 효과를 구현하는데도 `flutter_reorderable_list`를 함께 사용할 수 있습니다.

더 자세한 정보는 [`flutter_reorderable_list` 공식 문서](https://pub.dev/packages/flutter_reorderable_list)를 참고해주세요.