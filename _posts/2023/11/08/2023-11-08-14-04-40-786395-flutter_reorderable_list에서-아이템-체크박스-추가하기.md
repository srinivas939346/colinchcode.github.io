---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 체크박스 추가하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

때때로 앱에서 사용자가 아이템을 선택하고 순서를 변경하는 기능이 필요할 수 있습니다. Flutter에서는 `flutter_reorderable_list` 패키지를 사용하여 이러한 기능을 구현할 수 있습니다. 이 패키지는 아이템을 재정렬하고 순서를 유연하게 변경할 수 있는 리스트 위젯을 제공합니다.

하지만 원하는 경우에는 각 아이템에 체크박스를 추가하여 사용자가 선택할 수 있도록 할 수도 있습니다. 이 문서에서는 `flutter_reorderable_list` 위젯에 아이템 체크박스를 추가하는 방법을 알아보겠습니다.

## 1. 패키지 가져오기

먼저, `flutter_reorderable_list` 패키지를 프로젝트에 추가해야 합니다. `pubspec.yaml` 파일을 열고 `dependencies` 섹션에 다음 코드를 추가합니다:

```yaml
dependencies:
  flutter_reorderable_list: ^0.2.3
```

그런 다음 터미널에서 `flutter pub get` 명령을 실행하여 패키지를 가져옵니다.

## 2. 아이템 체크박스 추가하기

이제 위젯에서 아이템 체크박스를 추가할 수 있습니다. `flutter_reorderable_list` 패키지의 `ReorderableListView` 위젯을 사용하여 아이템 리스트를 생성합니다. 각 아이템 위젯은 체크박스와 사용자 지정 컨텐츠로 구성됩니다. 

다음은 아이템 체크박스를 추가한 예시 코드입니다:

```dart
ReorderableListView(
  onReorder: (int oldIndex, int newIndex) {
    // 아이템 재정렬 로직
  },
  children: List.generate(itemCount, (index) {
    return ListTile(
      key: Key('$index'),
      leading: Checkbox(
        onChanged: (bool? value) {
          // 체크박스 상태 변경 로직
        },
        value: isChecked[index],
      ),
      title: Text('Item $index'),
    );
  }),
);
```

위 코드에서 `itemCount`는 리스트의 아이템 개수를 나타내며, `isChecked`는 각 아이템의 체크 상태를 저장하는 리스트입니다. `onReorder` 콜백 함수를 사용하여 아이템을 재정렬하고, 각 아이템 위젯의 `Checkbox` 위젯을 사용하여 체크 상태를 토글할 수 있습니다.

## 3. 추가 기능 구현하기

위 예시 코드를 기반으로 추가적인 기능을 구현할 수 있습니다. 예를 들어, 체크박스를 토글할 때마다 해당 아이템을 선택 상태로 표시하고 리스트의 다른 요소에 영향을 줄 수 있습니다.

아이템 체크박스를 사용하여 리스트의 아이템을 선택하고 순서를 변경하는 기능은 앱의 유용한 기능 중 하나입니다. Flutter의 `flutter_reorderable_list` 패키지를 사용하면 이러한 기능을 간단하게 구현할 수 있습니다.