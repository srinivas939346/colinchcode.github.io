---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 필터링하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

## 개요
`flutter_reorderable_list` 패키지는 Flutter 앱에서 아이템을 재정렬할 수 있는 기능을 제공합니다. 그러나 때로는 특정 조건에 따라 아이템을 필터링하고 싶을 수 있습니다. 이 블로그 포스트에서는 `flutter_reorderable_list`에서 아이템을 필터링하는 방법에 대해 알아보겠습니다.

## 필터링 방법
1. 먼저, `flutter_reorderable_list` 패키지를 프로젝트에 추가합니다. 이를 위해 `pubspec.yaml` 파일에 다음과 같은 의존성을 추가하세요:

   ```yaml
   dependencies:
     flutter_reorderable_list: ^0.2.0
   ```

2. 필터링하려는 아이템의 속성을 정의하세요. 예를 들어, 다음과 같은 `Item` 클래스가 있다고 가정해보겠습니다:

   ```dart
   class Item {
     String title;
     bool isVisible;
     
     Item({required this.title, required this.isVisible});
   }
   ```

3. `flutter_reorderable_list` 위젯을 사용하여 아이템 목록을 만드세요. 필터링을 적용하기 위해 `List<Item>`을 `StreamBuilder`로 감싸줍니다. 필요에 따라 `StreamBuilder`의 `stream`에 적절한 `Stream`을 제공하세요:

   ```dart
   ReorderableList(
     onReorder: (oldIndex, newIndex) {
       // 아이템의 순서를 재정렬하는 로직 작성
     },
     child: StreamBuilder<List<Item>>(
       stream: // 필터링된 아이템 목록 스트림,
       initialData: // 초기 데이터,
       builder: (context, snapshot) {
         if (!snapshot.hasData) {
           return CircularProgressIndicator();
         }
         
         final visibleItems = snapshot.data!.where((item) => item.isVisible).toList();
         
         return ListView.builder(
           itemCount: visibleItems.length,
           itemBuilder: (context, index) {
             final item = visibleItems[index];
             return ListTile(
               title: Text(item.title),
             );
           },
         );
       }
     ),
   )
   ```

4. 필터링 로직을 구현합니다. 예를 들어, `isVisible` 속성을 기준으로 아이템을 필터링하고 싶다면, `Stream`에서 필터링된 아이템 목록을 반환하는 메서드를 정의하세요:

   ```dart
   Stream<List<Item>> getFilteredItems() {
     // 필터링 로직 작성
   }
   ```

5. `StreamBuilder`의 `stream` 속성에 `getFilteredItems()` 메서드를 제공하고 필요한 경우 `initialData`를 설정하세요:

   ```dart
   StreamBuilder<List<Item>>(
     stream: getFilteredItems(),
     initialData: [], // 초기 데이터 설정
     builder: (context, snapshot) {
       // snapshot 데이터를 사용하여 UI 빌드
     },
   )
   ```

## 결론
이제 `flutter_reorderable_list` 패키지에서 아이템을 필터링하는 방법을 알게 되었습니다. 필요에 따라 원하는 조건에 맞게 아이템을 필터링하여 앱을 개발할 수 있습니다.

## 참고 자료
- [flutter_reorderable_list 패키지](https://pub.dev/packages/flutter_reorderable_list)
- [Flutter StreamBuilder 문서](https://api.flutter.dev/flutter/widgets/StreamBuilder-class.html)