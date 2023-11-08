---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 드래그 종료 이벤트 처리하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

`flutter_reorderable_list` 패키지는 플러터에서 아이템을 재정렬 가능한 리스트를 구현하기 위한 도구입니다. 이 패키지를 사용하면 사용자가 아이템을 드래그하여 순서를 변경할 수 있습니다. 그러나 아이템 드래그가 종료될 때 추가적인 작업을 수행하기 위해서는 이벤트를 처리해야 합니다.

## 이벤트 처리를 위한 준비

우선 `flutter_reorderable_list` 패키지를 프로젝트에 추가해야 합니다. `pubspec.yaml` 파일을 열고 `dependencies` 섹션에 다음과 같이 패키지를 추가합니다:

```yaml
dependencies:
  flutter_reorderable_list: ^0.2.2
```

그런 다음 패키지를 설치하기 위해 터미널에서 `flutter pub get` 명령을 실행합니다.

## 이벤트 처리 방법

`flutter_reorderable_list` 패키지에서 아이템 드래그 종료 이벤트를 처리하기 위해서는 `onReorder` 콜백을 사용합니다. `onReorder` 콜백은 아이템의 드래그를 종료한 후 호출됩니다. 이때, `oldIndex`와 `newIndex` 매개변수를 받게 되는데, 이는 이동 전의 인덱스와 이동 후의 인덱스를 나타냅니다.

다음은 `onReorder` 콜백을 가진 `ReorderableList` 위젯의 예제입니다:

```dart
ReorderableList(
  onReorder: (oldIndex, newIndex) {
    // 드래그 종료 이벤트 발생 시 수행할 작업
    // ...
  },
  // ...
)
```

위의 예제에서 `onReorder` 콜백에서는 아이템의 드래그 종료 이벤트가 발생한 후 수행할 작업을 구현하면 됩니다. 이때, `oldIndex`와 `newIndex`를 통해 이동된 아이템의 인덱스를 확인하고 적절한 작업을 수행하면 됩니다.

## 추가 정보

`flutter_reorderable_list` 패키지에 대한 자세한 내용은 [공식 문서](https://pub.dev/packages/flutter_reorderable_list)를 참조하십시오.

이제 당신은 `flutter_reorderable_list` 패키지를 사용하여 아이템 드래그 종료 이벤트를 처리할 수 있습니다. 이를 통해 사용자가 아이템의 순서를 쉽게 변경할 수 있는 기능을 구현할 수 있습니다.