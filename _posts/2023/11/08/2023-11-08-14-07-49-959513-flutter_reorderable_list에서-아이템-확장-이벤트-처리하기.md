---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 확장 이벤트 처리하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

[flutter_reorderable_list](https://pub.dev/packages/flutter_reorderable_list)는 Flutter에서 아이템을 재정렬할 수 있는 위젯입니다. 이 패키지를 사용하면 사용자가 아이템을 드래그하여 순서를 변경할 수 있습니다. 그러나 아이템을 확장하여 추가 정보를 표시하고 싶은 경우에는 어떻게 처리해야 할까요? 이 문제를 해결하기 위해 `flutter_reorderable_list`의 `onReorder` 콜백을 사용할 수 있습니다.

## 아이템 확장 처리

1. 먼저, flutter_reorderable_list를 설치해야 합니다. `pubspec.yaml` 파일에 다음과 같이 패키지를 추가해 주세요:

```yaml
dependencies:
  flutter_reorderable_list: ^0.2.0
```

2. 아이템 목록을 위한 `List` 변수를 생성합니다. 각 아이템은 `MyItem` 클래스로 정의되어 있어야 합니다. 이 클래스는 `key`와 `expanded`라는 두 가지 속성을 가집니다.

```dart
class MyItem {
  final String key;
  bool expanded;

  MyItem({
    required this.key,
    this.expanded = false,
  });
}
```

3. `StatefulWidget`를 사용하여 위젯을 생성합니다. 이 위젯은 `ReorderableList` 위젯과 `ListView.builder`를 사용하여 아이템 목록을 표시합니다. 아이템이 확장되어 있는 경우 추가 정보를 표시해야 하므로 `Visibility` 위젯을 사용합니다.

```dart
class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  List<MyItem> _items = [
    MyItem(key: 'Item 1'),
    MyItem(key: 'Item 2'),
    MyItem(key: 'Item 3'),
  ];

  @override
  Widget build(BuildContext context) {
    return ReorderableList(
      onReorder: (int oldIndex, int newIndex) {
        setState(() {
          if (oldIndex < newIndex) {
            newIndex -= 1;
          }
          final item = _items.removeAt(oldIndex);
          _items.insert(newIndex, item);
        });
      },
      child: ListView.builder(
        itemCount: _items.length,
        itemBuilder: (context, index) {
          final item = _items[index];
          return ReorderableItem(
            key: Key(item.key),
            childBuilder: (context, state) {
              return Card(
                key: Key(item.key),
                child: Column(
                  children: [
                    ListTile(
                      title: Text(item.key),
                      trailing: IconButton(
                        onPressed: () {
                          setState(() {
                            item.expanded = !item.expanded;
                          });
                        },
                        icon: Icon(item.expanded ? Icons.expand_less : Icons.expand_more),
                      ),
                    ),
                    Visibility(
                      visible: item.expanded,
                      child: Padding(
                        padding: EdgeInsets.all(10),
                        child: Text('Additional information'),
                      ),
                    ),
                  ],
                ),
              );
            },
          );
        },
      ),
    );
  }
}
```

4. 마지막으로, 위젯을 실행하여 화면에 아이템 목록이 표시되는지 확인해 보세요. 사용자가 아이템을 드래그하여 재정렬하고, 확장/축소 아이콘을 터치하여 아이템을 확장 또는 축소할 수 있습니다.

```dart
void main() {
  runApp(MaterialApp(
    home: MyWidget(),
  ));
}
```

이제 `flutter_reorderable_list`를 사용하여 아이템을 재정렬하고 확장 이벤트를 처리할 수 있습니다. 이를 사용하여 사용자가 아이템의 순서를 변경하고 추가 정보를 확인할 수 있는 유연한 Flutter 애플리케이션을 개발할 수 있습니다.