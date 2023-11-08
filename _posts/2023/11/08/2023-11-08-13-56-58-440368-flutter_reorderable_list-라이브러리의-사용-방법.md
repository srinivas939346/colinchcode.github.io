---
layout: post
title: "[flutter] flutter_reorderable_list 라이브러리의 사용 방법"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

## 소개
flutter_reorderable_list는 플러터(Flutter) 앱에서 아이템의 순서를 재배열할 수 있는 기능을 제공하는 라이브러리입니다. 이 라이브러리를 사용하면 리스트나 그리드와 같은 UI 요소에서 아이템들을 드래그하여 순서를 변경할 수 있습니다.

## 설치
먼저, `pubspec.yaml` 파일에 `flutter_reorderable_list` 라이브러리를 추가해야 합니다. 아래의 코드를 `dependencies` 섹션에 추가하세요:

```dart
dependencies:
  flutter_reorderable_list: <latest_version>
```

그리고 `pub get` 명령을 통해 라이브러리를 다운로드 받습니다.

## 사용 방법
1. `FlutterReorderableList` 위젯을 사용하여 정렬 가능한 리스트를 생성합니다. `children` 속성에는 정렬 가능한 아이템 위젯들의 리스트를 전달합니다.
```dart
FlutterReorderableList(
  children: <Widget>[
    // 정렬 가능한 아이템 위젯들
  ],
)
```
  
2. 각 아이템 위젯은 `ReorderableItem`으로 감싸야 합니다. `key` 속성은 아이템의 고유한 식별자로 사용됩니다.
```dart
ReorderableItem(
  key: UniqueKey(),
  child: Container(
    // 아이템의 내용
  ),
)
```

3. 필요에 따라 아이템의 배경색이나 그림자 등을 설정할 수 있습니다.
```dart
ReorderableItem(
  key: UniqueKey(),
  child: Container(
    // 아이템의 내용
  ),
  decoration: BoxDecoration(
    color: Colors.white,   // 배경색
    boxShadow: [
      BoxShadow(
        color: Colors.grey.withOpacity(0.5),
        spreadRadius: 1,
        blurRadius: 5,
        offset: Offset(0, 3),
      ),
    ],
    borderRadius: BorderRadius.circular(5),   // 테두리 둥글기
  ),
)
```

4. 순서 변경 시 호출될 콜백 함수를 설정합니다. `onReorder` 속성에 콜백 함수를 전달합니다.
```dart
FlutterReorderableList(
  children: <Widget>[
    // 정렬 가능한 아이템 위젯들
  ],
  onReorder: (int oldIndex, int newIndex) {
    // 순서 변경 시 호출될 로직
  },
)
```

## 예제 코드
아래는 `flutter_reorderable_list` 라이브러리의 사용 예제입니다.

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
      title: 'Reorderable List Example',
      home: ReorderableListExample(),
    );
  }
}

class ReorderableListExample extends StatefulWidget {
  @override
  _ReorderableListExampleState createState() => _ReorderableListExampleState();
}

class _ReorderableListExampleState extends State<ReorderableListExample> {
  List<String> items = ['Item 1', 'Item 2', 'Item 3', 'Item 4', 'Item 5'];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Reorderable List Example'),
      ),
      body: FlutterReorderableList(
        children: items
            .map((item) => ReorderableItem(
                  key: Key(item),
                  child: ListTile(
                    title: Text(item),
                  ),
                ))
            .toList(),
        onReorder: (int oldIndex, int newIndex) {
          setState(() {
            if (newIndex > oldIndex) {
              newIndex -= 1;
            }
            final item = items.removeAt(oldIndex);
            items.insert(newIndex, item);
          });
        },
      ),
    );
  }
}
```

이 예제는 `MyApp` 클래스에 `ReorderableListExample` 위젯을 생성하여 사용합니다. 위젯은 `Scaffold`에 `FlutterReorderableList`를 포함하고 있으며, 아이템은 `ListTile`로 구성됩니다. 아이템의 순서 변경 시 `onReorder` 콜백 함수가 호출됩니다.

## 참고 자료
- [flutter_reorderable_list 라이브러리](https://pub.dev/packages/flutter_reorderable_list)
- [플러터(Flutter) 공식 문서](https://flutter.dev/)