---
layout: post
title: "[flutter] flutter_reorderable_list 라이브러리 소개"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

_이번 블로그에서는 `flutter_reorderable_list` 라이브러리에 대한 소개를 해보겠습니다._

## 소개

`flutter_reorderable_list`는 Flutter 앱에서 드래그 앤 드롭 가능한(Reorderable) 리스트를 만들 수 있게 도와주는 라이브러리입니다. 이 라이브러리를 사용하면 사용자가 리스트 항목을 원하는 순서로 재정렬하는 기능을 손쉽게 구현할 수 있습니다.

## 주요 특징

- 드래그 앤 드롭을 통한 리스트 재정렬
- 다양한 사용자 정의 가능
- 터치 및 스와이프 제스처 지원
- 다양한 리스트 타입에 대한 지원 (리스트뷰, 그리드뷰 등)
- 쉬운 통합

## 설치 방법

`pubspec.yaml` 파일에 아래의 디펜던시를 추가해주세요:

```yaml
dependencies:
  flutter_reorderable_list: ^1.0.0
```

그리고 실행하기 전에 패키지를 업데이트 해줍니다.

```bash
$ flutter packages get
```

## 사용 방법

다음은 `flutter_reorderable_list`를 사용하여 드래그 앤 드롭 가능한 리스트를 생성하는 예시입니다.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';

class ReorderableListExample extends StatefulWidget {
  @override
  _ReorderableListExampleState createState() => _ReorderableListExampleState();
}

class _ReorderableListExampleState extends State<ReorderableListExample> {
  List<String> items = [
    'Item 1',
    'Item 2',
    'Item 3',
    'Item 4',
    'Item 5',
  ];

  @override
  Widget build(BuildContext context) {
    return ReorderableList(
      onReorder: (oldIndex, newIndex) {
        setState(() {
          if (newIndex > oldIndex) {
            newIndex -= 1;
          }
          final item = items.removeAt(oldIndex);
          items.insert(newIndex, item);
        });
      },
      child: ListView(
        children: items
            .map((item) => ListTile(
                  key: Key(item),
                  title: Text(item),
                ))
            .toList(),
      ),
    );
  }
}
```

위의 코드에서는 `ReorderableList`와 `ListView`를 사용하여 드래그 앤 드롭 가능한 리스트를 생성하였습니다. `onReorder` 콜백 함수를 통해 재정렬이 일어날 때마다 리스트의 순서를 업데이트하도록 구현하였습니다.

## 결론

`flutter_reorderable_list`는 간편하게 드래그 앤 드롭 가능한 리스트를 구현할 수 있는 탁월한 라이브러리입니다. 이 라이브러리를 사용하면 Flutter 앱에서 보다 유저 친화적인 인터페이스를 제공할 수 있으며, 사용자가 원하는 순서로 리스트를 재정렬하는 기능을 쉽게 구현할 수 있습니다. 자세한 사용 방법은 공식 문서를 참고해보세요.

- 공식 문서: [flutter_reorderable_list GitHub](https://github.com/luisp343/flutter_reorderable_list)