---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 이미지 삽입하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

이 문서에서는 `flutter_reorderable_list` 패키지를 사용하여 Flutter 앱에서 아이템 이미지를 삽입하는 방법에 대해 다룹니다.

## 패키지 설치

먼저, `flutter_reorderable_list` 패키지를 프로젝트에 추가해야 합니다. `pubspec.yaml` 파일에 다음과 같이 패키지를 추가합니다:

```yaml
dependencies:
  flutter_reorderable_list: ^0.2.0
```

그런 다음 터미널에서 `flutter packages get` 명령어를 실행하여 패키지를 가져옵니다.

## 아이템 이미지 삽입하기

`flutter_reorderable_list`는 `ReorderableListView` 위젯을 제공합니다. 이 위젯을 사용하여 아이템 리스트를 만들고 아이템에 이미지를 삽입할 수 있습니다.

먼저, `ReorderableListView.builder`를 사용하여 아이템 리스트를 빌드할 수 있습니다. 아래는 예시 코드입니다:

```dart
ReorderableListView.builder(
  itemCount: items.length,
  itemBuilder: (BuildContext context, int index) {
    final item = items[index];
    return ListTile(
      key: Key(item['id']),
      leading: Image.network(item['imageUrl']),
      title: Text(item['title']),
    );
  },
  onReorder: (int oldIndex, int newIndex) {
    // 리스트 아이템을 재정렬하는 로직을 구현합니다.
    // ...
  },
)
```

위 예시 코드에서 `itemBuilder` 콜백 함수에서 각 아이템의 이미지를 `Image.network` 위젯으로 삽입하고 있습니다. `item['imageUrl']`은 아이템에 대한 이미지 URL을 참조하도록 설정해야 합니다.

`onReorder` 콜백 함수를 사용하여 아이템을 재정렬할 수 있습니다. 이 함수는 아이템의 이전 인덱스와 새로운 인덱스를 인수로 받으며, 재정렬하는 로직을 구현할 수 있습니다.

## 결론

`flutter_reorderable_list` 패키지를 사용하여 Flutter 앱에서 아이템 이미지를 삽입하는 방법을 배웠습니다. 이를 통해 사용자 인터페이스를 향상시키고, 사용자가 아이템을 자유롭게 재정렬할 수 있는 기능을 제공할 수 있습니다.

더 자세한 정보는 [flutter_reorderable_list GitHub 저장소](https://github.com/hanshengchiu/flutter_reorderable_list)를 참고하세요.