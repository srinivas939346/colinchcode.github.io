---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 정렬하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

이번 글에서는 Flutter에서 아이템을 정렬하기 위해 `flutter_reorderable_list` 라이브러리를 사용하는 방법에 대해 알아보겠습니다.

## 1. flutter_reorderable_list 소개

`flutter_reorderable_list`는 Flutter에서 리레이아웃을 변경하고 아이템을 재정렬하는 기능을 제공하는 라이브러리입니다. 이 라이브러리를 사용하면 사용자가 화면 상의 아이템을 드래그하여 순서를 변경할 수 있습니다.

## 2. 설치 및 설정

`pubspec.yaml` 파일을 열고 다음과 같이 `flutter_reorderable_list` 패키지를 추가합니다.

```yaml
dependencies:
  flutter_reorderable_list: ^0.2.0
```

그리고 패키지를 적용할 페이지에서 `flutter_reorderable_list`를 import 합니다.

```dart
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';
```

## 3. 리레이아웃 정의하기

`flutter_reorderable_list`를 사용하여 정렬 가능한 아이템을 포함하는 리레이아웃을 정의하기 위해 `ReorderableList` 위젯을 사용합니다. 예를 들어, 다음과 같이 `ListView` 위젯을 감싸는 형태로 리레이아웃을 구성할 수 있습니다.

```dart
ReorderableList(
  onReorder: (int oldIndex, int newIndex) {
    // 아이템이 재정렬될 때 호출되는 콜백 함수
    // 작성해야 할 로직을 구현합니다.
  },
  child: ListView(
    children: <Widget>[
      // 정렬 가능한 아이템들을 리스트에 추가합니다.
    ],
  ),
)
```

위 예제에서 `onReorder` 콜백 함수는 아이템이 재정렬될 때 호출됩니다. 이곳에서 아이템의 순서를 변경하는 로직을 구현할 수 있습니다.

## 4. 아이템 정렬하기

`flutter_reorderable_list`를 통해 아이템을 정렬하기 위해서는 내부적으로 사용하는 데이터 구조에 대한 처리가 필요합니다. 일반적으로는 리스트에 대한 상태를 관리하는 State 클래스를 만들고, 이 클래스에서 아이템의 순서를 변경하는 로직을 구현합니다.

```dart
class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  List<String> items = ['Item 1', 'Item 2', 'Item 3'];

  @override
  Widget build(BuildContext context) {
    return ReorderableList(
      onReorder: (int oldIndex, int newIndex) {
        setState(() {
          if (newIndex > oldIndex) {
            newIndex -= 1;
          }
          final item = items.removeAt(oldIndex);
          items.insert(newIndex, item);
        });
      },
      child: ListView.builder(
        itemCount: items.length,
        itemBuilder: (BuildContext context, int index) {
          return ListTile(
            key: Key('$index'),
            title: Text(items[index]),
          );
        },
      ),
    );
  }
}
```

위 예제에서는 `MyWidget`이 `StatefulWidget`을 상속하며, `items` 리스트에 아이템을 기록합니다. 그리고 `onReorder` 콜백 함수에서 `setState`를 사용하여 상태를 업데이트하고, 아이템을 재정렬합니다. `ListView.builder`를 사용하여 아이템들을 보여줍니다.

이렇게 구성하면 사용자는 앱에서 아이템들을 드래그하여 순서를 변경할 수 있습니다.

## 5. 마무리

이번에는 `flutter_reorderable_list` 라이브러리를 통해 Flutter에서 아이템을 정렬하는 방법에 대해 알아보았습니다. 이 라이브러리를 사용하면 사용자 친화적인 UI를 구성할 수 있고, 원하는 기능을 구현할 수 있습니다.

더 자세한 정보는 [flutter_reorderable_list GitHub 페이지](https://github.com/hanshengchiu/flutter_reorderable_list)를 참고하시기 바랍니다.