---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 버튼 추가하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

`flutter_reorderable_list`는 Flutter에서 사용할 수 있는 샘플 프로젝트의 일부로서, 아이템을 재정렬할 수 있는 기능을 제공합니다. 이 라이브러리를 사용하여 아이템들을 재정렬할 수 있는 UI를 구현할 수 있습니다. 그러나 기본적으로는 재정렬만 가능하며, 아이템을 삭제하거나 편집하는 기능은 제공하지 않습니다.

이번에는 `flutter_reorderable_list`에 아이템 버튼을 추가하는 방법에 대해 알아보겠습니다. 이를 통해 재정렬 뿐만 아니라 아이템을 삭제하거나 편집하는 기능을 추가할 수 있습니다.

## 1. `flutter_reorderable_list` 설치하기

우선 `flutter_reorderable_list`를 설치해야 합니다. `pubspec.yaml` 파일에 아래의 종속성을 추가해주세요.

```yaml
dependencies:
  flutter_reorderable_list: any
```

그리고 `pub get` 명령어를 사용하여 패키지를 가져옵니다.

## 2. 아이템 버튼 추가하기

아이템 버튼을 추가하기 위해서는 리스트 아이템을 위한 위젯을 커스텀해야 합니다. 예를 들어, 아이템 위젯을 `ReorderableItem`으로 감싸고, 그 안에 삭제 버튼이나 편집 버튼을 추가할 수 있습니다.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';

class MyListItem extends StatelessWidget {
  final int index;
  final Key key;
  final Widget child;

  MyListItem({required this.index, required this.key, required this.child});

  void _deleteItem() {
    // 아이템 삭제 로직 추가
  }

  void _editItem() {
    // 아이템 편집 로직 추가
  }

  @override
  Widget build(BuildContext context) {
    return ReorderableItem(
      key: key,
      // 재정렬을 위한 기본 위젯
      childBuilder: (context, state) {
        return Card(
          child: ListTile(
            title: child,
            trailing: Row(
              mainAxisSize: MainAxisSize.min,
              children: [
                IconButton(
                  icon: Icon(Icons.delete),
                  onPressed: _deleteItem,
                ),
                IconButton(
                  icon: Icon(Icons.edit),
                  onPressed: _editItem,
                ),
              ],
            ),
          ),
        );
      },
    );
  }
}
```

위의 코드에서 `MyListItem` 위젯은 재정렬이 가능한 리스트 아이템을 나타내는 위젯입니다. `ReorderableItem` 위젯으로 이를 감싸고, 그 안에 `ListTile` 위젯을 사용하여 리스트 아이템을 구성하고 있습니다. `trailing` 속성에 삭제 버튼과 편집 버튼을 추가하였습니다.

## 3. 아이템 삭제 및 편집 로직 추가하기

위의 예시 코드에서는 삭제 버튼과 편집 버튼을 추가하였지만, 아직 기능이 구현되어 있지 않습니다. 따라서 `MyListItem` 위젯에서 `_deleteItem`과 `_editItem` 메서드에 실제로 해당 로직을 추가해야 합니다. 이 메서드를 구현하여 아이템 삭제 및 편집 로직을 추가하세요.

## 마무리

이제 `flutter_reorderable_list`에 아이템 버튼을 추가하는 방법을 알아보았습니다. 이를 통해 재정렬 이외의 기능을 추가하여 좀 더 다양한 UI를 구현할 수 있습니다. 위의 예시를 참고하여 자신의 프로젝트에서도 적절한 버튼을 추가해보세요.

> 참고: [flutter_reorderable_list GitHub 레포지토리](https://github.com/hanshengchiu/flutter_reorderable_list)