---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 클릭 이벤트 처리하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

## 개요
flutter_reorderable_list는 플러터(Flutter)에서 이동 가능한 아이템 목록을 생성할 수 있는 패키지입니다. 이 패키지를 사용하면 사용자가 아이템을 드래그하여 재정렬할 수 있는 기능을 쉽게 구현할 수 있습니다. 하지만 기본적으로는 아이템 클릭 이벤트를 처리하는 기능은 제공되지 않습니다. 본 포스트에서는 flutter_reorderable_list에서 아이템 클릭 이벤트를 처리하는 방법에 대해 알아보겠습니다.

## 아이템 클릭 이벤트 처리 방법
flutter_reorderable_list에서 아이템 클릭 이벤트를 처리하기 위해선 아래와 같은 단계를 따라야 합니다.

1. ReorderableSliverList 위젯을 사용하여 이동 가능한 아이템 목록을 생성합니다.
2. 각 아이템 위젯에 GestureDetector를 추가하여 클릭 이벤트를 감지합니다.
3. GestureDetector의 onTap 콜백 함수에서 클릭 이벤트를 처리합니다.

아래는 아이템 클릭 이벤트를 처리하기 위한 예시 코드입니다.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Reorderable List Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  List<String> items = ['Item 1', 'Item 2', 'Item 3'];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Reorderable List Demo'),
      ),
      body: CustomScrollView(
        slivers: <Widget>[
          ReorderableSliverList(
            delegate: ReorderableSliverChildBuilderDelegate(
              (BuildContext context, int index) {
                return GestureDetector(
                  onTap: () {
                    // 클릭 이벤트 처리 로직 작성
                    print('Item $index clicked');
                  },
                  child: ListTile(
                    key: Key('$index'),
                    title: Text(items[index]),
                  ),
                );
              },
              childCount: items.length,
            ),
            onReorder: (int oldIndex, int newIndex) {
              // 아이템 재정렬 로직 작성
              setState(() {
                if (newIndex > oldIndex) {
                  newIndex -= 1;
                }
                final item = items.removeAt(oldIndex);
                items.insert(newIndex, item);
              });
            },
          ),
        ],
      ),
    );
  }
}
```

위 예시 코드에서는 `ReorderableSliverList`와 `GestureDetector`를 사용하여 아이템 목록을 생성하고 클릭 이벤트를 처리하였습니다. `onTap` 콜백 함수에서 클릭 이벤트를 처리할 수 있으며, 여기서는 단순히 'Item [index] clicked'를 출력하는 로직을 작성하였습니다.

## 결론
flutter_reorderable_list에서 아이템 클릭 이벤트를 처리하기 위해서는 `ReorderableSliverList`와 `GestureDetector`를 사용해야 합니다. 위 예시 코드를 참고하여 원하는 클릭 이벤트 처리 로직을 작성해보세요.