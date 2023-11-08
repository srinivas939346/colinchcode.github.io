---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 스와이프 이벤트 처리하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

`flutter_reorderable_list`는 Flutter에서 리스트 아이템의 재정렬을 가능하게 해주는 패키지입니다. 이 패키지를 사용하면 사용자가 리스트 아이템을 드래그 앤 드롭하여 순서를 변경할 수 있습니다. 하지만 기본적으로 `flutter_reorderable_list`는 아이템 스와이프에 대한 이벤트 처리를 지원하지 않습니다.

그러나 우리는 `flutter_reorderable_list`와 함께 `Dismissible` 위젯을 사용하여 아이템 스와이프 이벤트를 처리할 수 있습니다. 이를 통해 사용자가 리스트 아이템을 스와이프하여 삭제 또는 기타 작업을 수행할 수 있게 됩니다.

아래는 `flutter_reorderable_list`와 `Dismissible`를 함께 사용하여 아이템 스와이프 이벤트를 처리하는 예시 코드입니다.

```dart
ReorderableListView(
  // 아이템 재정렬을 위한 소스 데이터 리스트
  children: List.generate(items.length, (index) {
    return Dismissible(
      // 키를 사용하여 유일한 식별자로 지정
      key: Key(items[index]),
      // 아이템을 스와이프할 때 호출되는 콜백
      onDismissed: (direction) {
        setState(() {
          // 아이템 삭제 처리
          items.removeAt(index);
        });
      },
      child: ListTile(
        title: Text(items[index]),
      ),
    );
  }),
  // 아이템 재정렬을 위한 콜백
  onReorder: (oldIndex, newIndex) {
    setState(() {
      // 아이템 재정렬 처리
      if (newIndex > oldIndex) newIndex -= 1;
      final String item = items.removeAt(oldIndex);
      items.insert(newIndex, item);
    });
  },
);
```

위의 코드에서 `Dismissible` 위젯의 `key` 속성을 사용하여 아이템을 고유하게 식별하고, `onDismissed` 콜백을 사용하여 아이템을 삭제하도록 설정했습니다. 또한 `ReorderableListView`의 `onReorder` 콜백을 사용하여 아이템을 재정렬하도록 설정했습니다.

이제 `flutter_reorderable_list`와 `Dismissible`를 함께 사용하여 리스트 아이템의 스와이프 이벤트를 처리할 수 있습니다. 이를 통해 사용자에게 더 편리한 리스트 사용 경험을 제공할 수 있습니다.

## 참고 자료
- [flutter_reorderable_list 패키지](https://pub.dev/packages/flutter_reorderable_list)
- [Dismissible 위젯](https://api.flutter.dev/flutter/widgets/Dismissible-class.html)