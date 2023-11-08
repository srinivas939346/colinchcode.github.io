---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 폰트 설정하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

## 개요
flutter_reorderable_list는 Flutter에서 사용자가 아이템의 순서를 재정렬 할 수 있는 위젯입니다. 이 위젯을 사용하여 아이템을 표시할 때, 폰트를 설정하는 방법을 알아보겠습니다.

## 폰트 설정하기
flutter_reorderable_list를 사용하여 아이템을 표시하는 경우, ListTile 위젯을 사용할 수 있습니다. ListTile 위젯의 title 속성을 사용하여 폰트를 설정할 수 있습니다.

예를 들어, 다음과 같이 ListTile 위젯을 사용하여 아이템을 표시하고 폰트를 설정할 수 있습니다:

```dart
ReorderableList(
    onReorder: (oldIndex, newIndex) {
        // 순서 재정렬 로직
    },
    scrollDirection: Axis.vertical,
    children: <Widget>[
        for (var item in itemList)
            ListTile(
                key: ValueKey(item.id),
                title: Text(
                    item.title,
                    style: TextStyle(
                        fontSize: 16,
                        fontWeight: FontWeight.bold,
                    ),
                ),
            ),
    ],
)
```

위의 코드에서는 ListTile의 title 속성을 사용하여 폰트를 설정하고 있습니다. TextStyle의 fontSize와 fontWeight 속성을 사용하여 원하는 폰트 스타일을 지정할 수 있습니다.

## 결론
flutter_reorderable_list에서 아이템의 폰트를 설정하는 방법을 알아보았습니다. ListTile 위젯의 title 속성을 사용하여 폰트를 설정할 수 있으며, TextStyle을 사용하여 원하는 폰트 스타일을 지정할 수 있습니다.

## 참고 자료
- [flutter_reorderable_list 패키지](https://pub.dev/packages/flutter_reorderable_list)
- [Flutter 공식 문서](https://flutter.dev/)