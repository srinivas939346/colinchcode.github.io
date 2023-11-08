---
layout: post
title: "[flutter] flutter_reorderable_list에서 아이템 검색하기"
description: " "
date: 2023-11-08
tags: [flutter]
comments: true
share: true
---

이번 글에서는 플러터(Flutter)의 `flutter_reorderable_list` 패키지에서 아이템을 검색하는 방법에 대해 알아보겠습니다.

## flutter_reorderable_list 패키지란?

`flutter_reorderable_list` 패키지는 플러터에서 드래그 앤 드롭을 통해 아이템의 순서를 변경할 수 있는 리스트를 구현할 때 사용되는 패키지입니다. 이 패키지를 사용하면 사용자가 간편하게 리스트 아이템을 재정렬할 수 있습니다.

## 아이템 검색하기

`flutter_reorderable_list` 패키지에서는 아이템을 검색하는 기능을 내장하고 있지 않습니다. 그러나 아이템을 검색하고 싶은 경우 몇 가지 방법을 사용할 수 있습니다.

### 1. 리스트 필터링

리스트에서 특정 조건을 만족하는 아이템만을 보여주는 방법으로 검색 기능을 구현할 수 있습니다. 예를 들어, 아이템의 이름이 특정 문자열을 포함하고 있는 경우 해당 아이템만을 출력하도록 리스트를 필터링할 수 있습니다.

```dart
// 아이템 리스트
List<String> items = ["apple", "banana", "grape", "orange"];

// 특정 문자열을 포함하는 아이템만 필터링
List<String> filteredItems = items.where((item) => item.contains("a")).toList();

// 필터링된 아이템 출력
filteredItems.forEach((item) => print(item));
```

위의 예시에서는 `items` 리스트에서 이름에 "a"를 포함하는 아이템들만을 필터링하여 `filteredItems` 리스트에 저장한 후 출력하였습니다.

### 2. 검색 위젯 추가

`flutter_reorderable_list` 패키지를 사용할 때, 아이템을 검색하는 위젯을 추가로 구현할 수도 있습니다. 이 경우, 검색 위젯을 통해 사용자가 검색어를 입력하면 해당 검색어를 포함하는 아이템들만을 보여줄 수 있습니다.

검색 위젯의 구현 방법은 다양할 수 있으며, 플러터의 다른 패키지를 활용하거나 커스텀 위젯을 디자인하여 사용할 수 있습니다. 예를 들어, `flutter_search_bar` 패키지를 사용하여 간단한 검색 위젯을 구현하고 아이템을 검색할 수 있습니다.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_search_bar/flutter_search_bar.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: SearchBarDemo(),
    );
  }
}

class SearchBarDemo extends StatefulWidget {
  @override
  _SearchBarDemoState createState() => _SearchBarDemoState();
}

class _SearchBarDemoState extends State<SearchBarDemo> {
  // 아이템 리스트
  List<String> items = ["apple", "banana", "grape", "orange"];
  
  // 검색어
  String searchTerm = "";

  // 검색 위젯 생성
  SearchBar searchBar;

  // 검색어 업데이트 시 처리
  void onSubmitted(String value) {
    setState(() {
      searchTerm = value;
    });
  }

  @override
  void initState() {
    super.initState();
    searchBar = SearchBar(
      inBar: false,
      setState: setState,
      onSubmitted: onSubmitted,
      buildDefaultAppBar: buildAppBar,
    );
  }

  @override
  Widget build(BuildContext context) {
    // 검색어를 포함하는 아이템들만 필터링
    List<String> filteredItems = items.where((item) => item.contains(searchTerm)).toList();
    
    return Scaffold(
      appBar: searchBar.build(context),
      body: ListView.builder(
        itemCount: filteredItems.length,
        itemBuilder: (context, index) => ListTile(
          title: Text(filteredItems[index]),
        ),
      ),
    );
  }

  // 커스텀 앱바 생성
  AppBar buildAppBar(BuildContext context) {
    return AppBar(
      title: Text('Search Bar Demo'),
      actions: [searchBar.getSearchAction(context)],
    );
  }
}
```

위의 예시에서는 `flutter_search_bar` 패키지를 사용하여 검색 위젯을 구현하고 있습니다. 사용자가 검색어를 입력하면 해당 검색어를 포함하는 아이템들만을 보여주도록 리스트를 필터링하여 출력합니다.

## 결론

`flutter_reorderable_list` 패키지에서 아이템을 검색하기 위해서는 리스트를 필터링하거나 검색 위젯을 추가로 구현하여 사용할 수 있습니다. 각각의 방법은 사용자의 요구에 맞춰 선택하여 구현하면 됩니다.