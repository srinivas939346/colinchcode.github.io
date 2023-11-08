---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템의 상태 저장하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

## 소개

flutter_reorderable_list는 플러터 앱에서 아이템을 사용자 정의 가능한 방식으로 정렬 할 수 있는 패키지입니다. 이 패키지를 사용하면 사용자가 목록의 아이템을 드래그하여 순서를 변경할 수 있습니다. 그러나 기본적으로 이 패키지는 아이템의 상태를 유지하지 않습니다. 즉, 순서를 변경할 때마다 아이템의 상태가 초기화됩니다.

이번 글에서는 flutter_reorderable_list를 사용하여 아이템의 상태를 저장하는 방법에 대해 알아보겠습니다.

## 구현

아이템의 상태를 저장하기 위해서는 상태를 나타내는 변수를 각 아이템에 추가해야 합니다. 이 변수는 아이템을 표현하는 데이터 모델과 함께 사용됩니다. 예를 들어, Todo 앱의 경우 다음과 같은 TodoItem 클래스를 사용할 수 있습니다.

```dart
class TodoItem {
  String title;
  bool completed;

  TodoItem({required this.title, this.completed = false});
}
```

위의 클래스는 각 할 일 항목의 제목과 완료 여부를 저장합니다.

그런 다음, flutter_reorderable_list를 사용하여 아이템을 표시하는 위젯을 작성합니다. 이 위젯은 각 아이템의 상태를 수정할 수 있도록 해야 합니다. 예를 들어, TodoItem 위젯은 다음과 같이 작성할 수 있습니다.

```dart
class TodoItemWidget extends StatelessWidget {
  final TodoItem item;

  const TodoItemWidget({Key? key, required this.item}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return ListTile(
      title: Text(item.title),
      leading: Checkbox(
        value: item.completed,
        onChanged: (value) {
          // 아이템의 상태를 변경하고 다시 렌더링
          item.completed = value ?? false;
          setState(() {});
        },
      ),
    );
  }
}
```

위의 위젯은 ListTile과 Checkbox 위젯을 통해 할 일 항목을 표시하고 완료 여부를 변경할 수 있도록 합니다.

## 저장 및 복원

아이템의 상태를 저장하기 위해서는 외부 저장소를 사용해야 합니다. 일반적으로는 데이터베이스나 파일 시스템을 사용하여 아이템의 상태를 보존할 수 있습니다. 이 예시에서는 간단하게 SharedPreferences를 사용하여 아이템의 상태를 저장하고 복원하겠습니다.

우선, SharedPreferences 패키지의 의존성을 추가하고 초기화하는 코드를 작성합니다.

```yaml
dependencies:
  flutter:
    sdk: flutter
  shared_preferences: ^2.0.10
```

```dart
import 'package:shared_preferences/shared_preferences.dart';

// SharedPreferences 인스턴스 생성
SharedPreferences prefs = await SharedPreferences.getInstance();
```

이제 상태를 저장하고 복원하는 코드를 작성합니다. 저장은 아이템의 상태를 변경하는 시점에서 이루어져야 하며, 복원은 앱이 시작될 때 이루어져야 합니다.

```dart
// 상태 저장
await prefs.setBool('completed_${item.title}', item.completed);

// 상태 복원
item.completed = prefs.getBool('completed_${item.title}') ?? false;
```

위의 코드는 각 아이템마다 completed_${item.title}의 키로 완료 상태를 저장하고, 복원할 때 해당 키로부터 상태를 읽어옵니다.

## 결론

flutter_reorderable_list를 사용하여 아이템의 순서를 변경할 때 아이템의 상태를 유지하려면, 각 아이템에 상태를 나타내는 변수를 추가하고 외부 저장소를 사용하여 상태를 저장 및 복원해야 합니다. 이 예시에서는 SharedPreferences를 사용하여 간단하게 상태를 저장하고 복원하는 방법을 알아보았습니다. 다양한 상태 관리 방법을 사용하여 앱에 적합한 방법을 선택할 수 있습니다.

## 참고 자료

- [flutter_reorderable_list 패키지](https://pub.dev/packages/flutter_reorderable_list)
- [SharedPreferences 패키지](https://pub.dev/packages/shared_preferences)