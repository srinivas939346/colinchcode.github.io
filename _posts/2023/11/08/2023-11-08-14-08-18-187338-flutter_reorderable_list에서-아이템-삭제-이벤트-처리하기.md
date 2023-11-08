---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 삭제 이벤트 처리하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

---

Flutter의 `flutter_reorderable_list` 패키지를 사용하면 사용자가 아이템을 재정렬하고 삭제하는 기능을 구현할 수 있습니다. 이번 글에서는 `flutter_reorderable_list` 패키지를 사용하여 아이템 삭제 이벤트를 처리하는 방법에 대해 알아보겠습니다.

## 1. 패키지 설치 및 설정

먼저, `flutter_reorderable_list` 패키지를 프로젝트에 추가해야 합니다. `pubspec.yaml` 파일에 다음과 같이 패키지를 추가합니다:

```yaml
dependencies:
  flutter_reorderable_list: ^0.2.0
```

이후 터미널에서 `flutter pub get` 명령어를 실행하여 패키지를 다운로드 받고 의존성을 설정합니다.

## 2. 아이템 삭제 이벤트 처리하기

아이템 삭제를 위해서는 `ReorderableList` 위젯의 `onReorder` 콜백을 사용해야 합니다. 이 콜백은 아이템이 재정렬될 때 호출됩니다. 다음은 아이템 삭제를 위한 예제 코드입니다:

```dart
ReorderableList(
  onReorder: (int oldIndex, int newIndex) {
    setState(() {
      if (newIndex > oldIndex) {
        newIndex -= 1; // Removing an item will shift the indices
      }
      // Perform item deletion here
      items.removeAt(oldIndex);
    });
  },
  children: List.generate(items.length, (index) {
    return ListTile(
      key: Key('$index'),
      title: Text('Item ${items[index]}'),
    );
  }),
)
```

위의 코드에서 `onReorder` 콜백 함수 내에 `items.removeAt(oldIndex)`를 사용하여 아이템을 삭제하고, 삭제된 아이템에 대한 인덱스를 조정합니다.

이제, 위젯 트리에 포함된 `ReorderableList` 위젯을 사용하여 아이템이 삭제되는 것을 확인할 수 있습니다.

## 3. 결론

이제 `flutter_reorderable_list` 패키지를 사용하여 아이템 삭제 이벤트를 처리하는 방법을 배웠습니다. 다양한 재정렬 및 삭제 기능을 구현할 수 있다는 점에서 이 패키지는 매우 유용합니다. 

더 많은 정보를 원하신다면 공식 [flutter_reorderable_list GitHub 페이지](https://github.com/FlutterReorderableList/flutter_reorderable_list)를 참조하세요.