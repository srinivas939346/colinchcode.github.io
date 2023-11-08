---
layout: post
title: "[flutter] flutter_reorderable_list로 위젯의 순서 변경하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

이번 글에서는 Flutter에서 위젯의 순서를 변경하는 방법 중 하나인 `flutter_reorderable_list` 패키지를 사용하는 방법에 대해서 알아보겠습니다.

## 1. 패키지 추가하기

먼저, `flutter_reorderable_list` 패키지를 사용하기 위해 `pubspec.yaml` 파일에 아래와 같이 패키지를 추가합니다:

```yaml
dependencies:
  flutter_reorderable_list: ^0.2.0
```

저장 후에는 터미널을 열고 `flutter packages get` 명령어를 입력하여 패키지를 다운로드 받습니다.

## 2. 위젯 생성하기

`flutter_reorderable_list` 패키지를 사용하여 위젯의 순서를 변경하기 위해서는 `ReorderableList`와 `ReorderableItem` 위젯을 작성해야 합니다. 

먼저, `ReorderableList`를 사용하여 위젯의 리스트를 생성하고, 순서를 변경할 수 있는 기능을 제공합니다.

```dart
ReorderableList(
  onReorder: (int oldIndex, int newIndex) {
    // 위젯의 순서 변경 로직 작성
  },
  child: ListView.builder(
    itemCount: widgetList.length,
    itemBuilder: (BuildContext context, int index) {
      return ReorderableItem(
        key: Key('$index'),
        childBuilder: (BuildContext context, ReorderableItemState state) {
          return ListTile(
            title: Text(widgetList[index].title),
            leading: Icon(Icons.widgets),
            trailing: Icon(Icons.reorder),
          );
        },
      );
    },
  ),
)
```

`ReorderableList`는 `onReorder` 콜백 함수를 제공하여 위젯의 순서가 변경될 때 호출될 수 있습니다. 이 콜백 함수에서는 위젯의 순서 변경에 대한 로직을 작성할 수 있습니다.

위 코드에서는 `ListView.builder`를 사용하여 위젯 리스트를 생성하고, 각 위젯은 `ReorderableItem`으로 생성됩니다. `key`를 통해 각각의 위젯을 식별하고, `childBuilder`를 통해 각 위젯의 모양을 설정할 수 있습니다.

## 3. 위젯 순서 변경하기

위젯의 순서를 변경할 수 있는 기능은 `ReorderableItem` 위젯에서 제공됩니다. 사용자는 위젯을 드래그하여 원하는 위치로 이동시킬 수 있습니다.

위젯의 순서를 변경할 때마다 `onReorder` 콜백 함수가 호출되므로, 이 함수에서 순서 변경에 대한 로직을 구현할 수 있습니다.

```dart
void onReorder(int oldIndex, int newIndex) {
  setState(() {
    if (newIndex > oldIndex) {
      newIndex -= 1;
    }
    final WidgetModel item = widgetList.removeAt(oldIndex);
    widgetList.insert(newIndex, item);
  });
}
```

위 코드에서는 `setState` 메소드를 호출하여 상태를 업데이트하고, `widgetList`라는 리스트에서 해당 위치의 위젯을 삭제하고 다시 삽입함으로써 순서를 변경합니다.

## 4. 결론

위와 같이 `flutter_reorderable_list` 패키지를 사용하면 Flutter에서 간단하게 위젯의 순서를 변경할 수 있습니다. `ReorderableList`와 `ReorderableItem` 위젯을 사용하여 위젯의 리스트를 생성하고, `onReorder` 콜백 함수를 통해 순서 변경 로직을 작성할 수 있습니다.

더 많은 정보와 사용 예제는 [flutter_reorderable_list의 공식 GitHub 페이지](https://github.com/fluttercommunity/flutter_reorderable_list)에서 확인할 수 있습니다.