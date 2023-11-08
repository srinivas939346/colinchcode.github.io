---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 확대/축소 가능하게 하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

일반적으로 아이템을 확대 또는 축소할 수 있는 기능은 사용자 경험을 향상시키는 데에 도움이 됩니다. 이번 블로그 포스트에서는 flutter_reorderable_list 패키지에서 아이템을 확대/축소할 수 있는 기능을 구현하는 방법에 대해 알아보겠습니다.

## `flutter_reorderable_list` 패키지란?

`flutter_reorderable_list`는 [Flutter](https://flutter.dev/)에서 사용할 수 있는 재배치 가능한 리스트를 제공하는 패키지입니다. 사용자가 아이템의 순서를 변경할 수 있는 기능을 구현할 수 있습니다.

## 아이템 확대/축소 기능 구현하기

1. 패키지를 프로젝트에 추가하기

   먼저, `flutter_reorderable_list` 패키지를 프로젝트에 추가합니다. `pubspec.yaml` 파일의 `dependencies` 섹션에 다음과 같이 패키지를 추가합니다:

   ```yaml
   dependencies:
     flutter_reorderable_list: ^0.2.0
   ```

   패키지를 추가한 후, `flutter packages get` 명령어를 실행하여 패키지를 다운로드 및 설치합니다.

2. 화면에 `ReorderableListView` 위젯 추가하기

   아이템 확대/축소 기능을 구현하기 위해 화면에 `ReorderableListView` 위젯을 추가합니다. 이 위젯은 재배치 가능한 리스트를 표시하는 역할을 합니다.

   ```dart
   ReorderableListView(
     children: [
       // 확대/축소 가능한 아이템 위젯들을 추가
     ],
     onReorder: (int oldIndex, int newIndex) {
       // 아이템의 순서 변경 시 실행할 코드
     },
   )
   ```

3. 아이템 위젯에 확대/축소 기능 추가하기

   아이템 위젯에 확대/축소 기능을 추가하기 위해 `InteractiveViewer` 위젯을 사용합니다. 이 위젯은 화면을 확대 및 축소하고 드래그할 수 있는 기능을 제공합니다.

   ```dart
   InteractiveViewer(
     child: // 확대/축소할 아이템 위젯
   ),
   ```

   위 코드를 `ReorderableListView` 위젯의 자식으로 추가하면 됩니다.

4. 아이템 순서 변경 시 실행할 코드 작성하기

   `ReorderableListView` 위젯의 `onReorder` 콜백 함수를 사용하여 아이템의 순서가 변경될 때 실행할 코드를 작성합니다. 이 예제에서는 아이템의 순서를 콘솔에 출력하는 예시를 보여줍니다.

   ```dart
   onReorder: (int oldIndex, int newIndex) {
     print("Item moved from $oldIndex to $newIndex");
   },
   ```

이제 위의 단계를 따라가면 `flutter_reorderable_list` 패키지를 사용하여 아이템을 확대/축소할 수 있는 기능을 구현할 수 있습니다. 사용자는 화면에서 아이템을 드래그하여 순서를 변경하고 확대/축소할 수 있게 될 것입니다.

더 자세한 내용은 [flutter_reorderable_list 패키지의 공식 문서](https://pub.dev/packages/flutter_reorderable_list)를 참조하세요.