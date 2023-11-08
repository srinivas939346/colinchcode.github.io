---
layout: post
title: "[flutter] flutter_reorderable_list를 활용한 실제 애플리케이션 예제"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

안녕하세요! 이번 포스트에서는 Flutter의 패키지인 `flutter_reorderable_list`를 활용하여 실제 애플리케이션에서 사용할 수 있는 예제를 소개하겠습니다. `flutter_reorderable_list`는 위젯을 재정렬할 수 있는 기능을 제공하며, 사용자가 목록을 원하는 순서대로 드래그하여 바꿀 수 있도록 도와줍니다. 

## 1. 패키지 설치

먼저, `flutter_reorderable_list` 패키지를 설치해야 합니다. `pubspec.yaml`파일에 아래의 의존성을 추가하고, 패키지를 가져와야 합니다.

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_reorderable_list: ^0.2.0
```

의존성을 추가한 후에는 `flutter pub get` 명령어를 실행하여 패키지를 가져옵니다.

## 2. 예제 애플리케이션 구현

이제 `flutter_reorderable_list`를 활용한 간단한 예제 애플리케이션을 만들어보겠습니다. 사용자가 그릇에 담을 수 있는 과일 목록을 재정렬할 수 있는 애플리케이션을 만들어보겠습니다.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_reorderable_list/flutter_reorderable_list.dart';

void main() {
  runApp(ReorderApp());
}

class ReorderApp extends StatefulWidget {
  @override
  _ReorderAppState createState() => _ReorderAppState();
}

class _ReorderAppState extends State<ReorderApp> {
  List<String> fruits = ['사과', '바나나', '오렌지', '수박', '포도'];

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('과일 재정렬'),
        ),
        body: ReorderableList(
          onReorder: (oldIndex, newIndex) {
            setState(() {
              if (oldIndex < newIndex) {
                newIndex -= 1;
              }
              final fruit = fruits.removeAt(oldIndex);
              fruits.insert(newIndex, fruit);
            });
          },
          child: ListView.builder(
            itemCount: fruits.length,
            itemBuilder: (context, index) {
              return ListTile(
                key: Key('$index'),
                title: Text(fruits[index]),
              );
            },
          ),
        ),
      ),
    );
  }
}
```

위의 코드에서는 `ReorderableList` 위젯을 사용하여 재정렬이 가능한 리스트를 생성합니다. `onReorder` 콜백을 이용하여 원하는 동작을 구현합니다. 해당 예제에서는 `fruits`라는 문자열 목록을 재정렬하고, `setState`를 호출하여 UI를 업데이트합니다. 

## 3. 실행 및 테스트

애플리케이션을 실행하여 과일 목록을 재정렬해보세요. 모양이 변경되는 것을 확인할 수 있습니다. 또한, 목록 순서가 콘솔에 출력되는지 확인해보세요.

## 4. 결론

이번 포스트에서는 `flutter_reorderable_list` 패키지를 사용하여 재정렬 가능한 리스트를 생성하는 예제를 살펴보았습니다. 이를 활용하여 다양한 애플리케이션에서 사용자 정의 목록을 구현할 수 있습니다.

더 많은 예제와 자세한 내용은 [flutter_reorderable_list GitHub 저장소](https://github.com/hanshengchiu/flutter_reorderable_list)를 참조해보세요.

이상으로 `flutter_reorderable_list`를 활용한 실제 애플리케이션 예제에 대해 알아보았습니다. 감사합니다!