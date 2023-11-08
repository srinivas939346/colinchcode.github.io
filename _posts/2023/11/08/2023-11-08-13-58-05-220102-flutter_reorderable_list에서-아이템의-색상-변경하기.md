---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템의 색상 변경하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

flutter_reorderable_list는 플러터에서 아이템을 드래그하여 순서를 바꿀 수 있는 위젯입니다. 이 위젯을 사용하여 리스트의 아이템의 색상을 변경하는 방법에 대해 알아보겠습니다.

## 1. flutter_reorderable_list 설치

먼저, 프로젝트에 flutter_reorderable_list 패키지를 설치해야 합니다. `pubspec.yaml` 파일에 아래와 같은 의존성을 추가합니다.

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_reorderable_list: ^0.2.0
```

의존성을 추가한 후, 패키지를 업데이트합니다.

```bash
flutter packages get
```

## 2. 아이템 위젯 생성

아이템 위젯을 생성하여 flutter_reorderable_list 위젯에 전달해줘야 합니다. 이때, 아이템의 색상을 변경할 수 있는 변수를 갖는 위젯을 만들어야 합니다. 예를 들어, 다음과 같은 `MyItem` 위젯을 생성합니다.

```dart
class MyItem extends StatelessWidget {
  final Color color;

  MyItem({required this.color});

  @override
  Widget build(BuildContext context) {
    return Container(
      width: double.infinity,
      height: 100,
      color: color,
      child: Center(
        child: Text(
          'Item',
          style: TextStyle(
            color: Colors.white,
            fontSize: 20,
          ),
        ),
      ),
    );
  }
}
```

위 코드에서는 `color` 변수를 통해 아이템의 색상을 설정합니다.

## 3. flutter_reorderable_list 사용

`MyItem` 위젯을 사용하여 flutter_reorderable_list를 생성하고 아이템의 색상을 변경할 수 있습니다. 아래는 예시 코드입니다.

```dart
class MyList extends StatefulWidget {
  @override
  _MyListState createState() => _MyListState();
}

class _MyListState extends State<MyList> {
  List<Color> itemColors = [
    Colors.red,
    Colors.blue,
    Colors.green,
  ];

  @override
  Widget build(BuildContext context) {
    return ReorderableListView(
      children: itemColors
          .map((color) => MyItem(color: color))
          .toList(),
      onReorder: (oldIndex, newIndex) {
        setState(() {
          if (oldIndex <= newIndex) {
            newIndex -= 1;
          }
          final item = itemColors.removeAt(oldIndex);
          itemColors.insert(newIndex, item);
        });
      },
    );
  }
}
```

위 코드에서는 `MyList` 위젯을 생성하여 `ReorderableListView`를 사용하고, `itemColors` 리스트를 반복하여 `MyItem` 위젯을 생성합니다. 아이템의 색상은 `itemColors` 리스트의 요소로 지정됩니다.

`onReorder` 콜백 함수에서 아이템의 순서가 변경될 때마다 상태를 업데이트하여 화면을 다시 그리도록 합니다.

## 4. 실행 결과 확인

위에서 작성한 코드를 실행하여 flutter_reorderable_list를 사용하여 아이템의 순서를 변경하고 아이템의 색상이 변경되는지 확인해보세요.

다른 질문이 있으시면 언제든지 알려주세요.