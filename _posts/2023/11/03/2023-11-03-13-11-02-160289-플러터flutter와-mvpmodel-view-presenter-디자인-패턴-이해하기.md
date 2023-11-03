---
layout: post
title: "[flutter] 플러터(Flutter)와 MVP(Model-View-Presenter) 디자인 패턴 이해하기"
description: " "
date: 2023-11-03
tags: [flutter]
comments: true
share: true
---

## 소개
플러터(Flutter)는 구글에서 개발한 UI 프레임워크로, 모바일 애플리케이션을 빠르고 쉽게 개발할 수 있도록 도와줍니다. 이러한 플러터 프레임워크는 MVC(Model-View-Controller) 패턴, MVP(Model-View-Presenter) 패턴 등 다양한 디자인 패턴을 사용하여 애플리케이션을 구조화합니다. 이번 블로그에서는 플러터와 MVP 디자인 패턴에 대해 자세히 알아보겠습니다.

## MVP 디자인 패턴
MVP는 Model-View-Presenter의 약자로, 뷰(View)와 비즈니스 로직인 프리젠터(Presenter)를 분리하여 구현하는 디자인 패턴입니다. 이 패턴은 애플리케이션을 구조화하여 유지보수와 테스트가 용이하도록 도와줍니다.

### 구성 요소
MVP 패턴은 크게 세 가지 구성 요소로 나뉩니다.

1. Model (모델): 데이터를 처리하는 부분으로, 비즈니스 로직과 데이터를 관리합니다.
2. View (뷰): 사용자 인터페이스를 구성하고, 사용자의 입력을 받아 그에 대한 결과를 표시합니다.
3. Presenter (프리젠터): 모델과 뷰를 연결하는 역할로, 사용자 입력을 받아 모델에게 전달하고, 모델의 결과를 받아 뷰에 표시합니다.

### 동작 방식
MVP 패턴은 다음과 같은 순서로 동작합니다.

1. 사용자는 뷰를 통해 입력을 하게 됩니다.
2. 뷰는 입력을 받아 프리젠터에게 전달합니다.
3. 프리젠터는 모델에게 입력을 전달합니다.
4. 모델은 입력을 처리하고 결과를 프리젠터에게 전달합니다.
5. 프리젠터는 결과를 받아 뷰에게 전달하여 표시합니다.

### 플러터에서의 MVP 패턴 적용
플러터에서 MVP 패턴을 적용하기 위해서는 다음과 같은 단계를 따릅니다.

1. 뷰(Widget)를 구현합니다.
2. 프리젠터(Presenter)를 작성합니다. 이때, 프리젠터는 뷰 인터페이스(View Interface)와 모델(Model)을 연결합니다.
3. 모델(Model)을 작성합니다. 모델은 데이터 처리와 비즈니스 로직을 담당합니다.
4. 뷰와 프리젠터, 모델을 연결하여 MVP 패턴을 완성합니다.

### 예시 코드
다음은 플러터에서 MVP 패턴을 적용한 예시 코드입니다.

#### 뷰 (View)
```dart
import 'package:flutter/material.dart';

class MyHomePage extends StatelessWidget {
  final String data;
  
  MyHomePage({required this.data});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('MVP Example'),
      ),
      body: Center(
        child: Text(data),
      ),
    );
  }
}
```

#### 프리젠터 (Presenter)
```dart
import 'package:flutter_mvp_example/models/data_model.dart';

class Presenter {
  final ViewInterface view;
  final Model model;

  Presenter({required this.view, required this.model});

  void fetchData() {
    String data = model.getData();
    view.updateData(data);
  }
}

abstract class ViewInterface {
  void updateData(String data);
}

class MyHomePagePresenter implements Presenter {
  final ViewInterface view;
  final Model model;

  MyHomePagePresenter({required this.view, required this.model});

  @override
  void fetchData() {
    String data = model.getData();
    view.updateData(data);
  }
}
```

#### 모델 (Model)
```dart
class Model {
  String getData() {
    return "Hello, MVP!";
  }
}
```

#### 앱 (App)
```dart
import 'package:flutter/material.dart';
import 'package:flutter_mvp_example/views/my_home_page.dart';
import 'package:flutter_mvp_example/presenters/my_home_page_presenter.dart';
import 'package:flutter_mvp_example/models/data_model.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  final Model model = Model();

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'MVP Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePagePresenter(
        view: MyHomePage(data: ''),
        model: model,
      ),
    );
  }
}
```

예시 코드를 작성한 이후에는 MyHomePagePresenter를 MyHomePage와 Model과 함께 연결해주는 작업을 진행합니다.

## 결론
이번 블로그에서는 플러터(Flutter)와 MVP(Model-View-Presenter) 디자인 패턴에 대해 간략히 알아보았습니다. MVP 패턴을 적용하면 플러터 애플리케이션의 구조화와 유지보수가 훨씬 용이해지며, 테스트도 편리하게 진행할 수 있습니다. 따라서, 플러터 개발을 할 때는 MVP 패턴을 고려하여 애플리케이션을 구현해보는 것이 좋습니다.

---
**참고 자료**
- Flutter: <https://flutter.dev>
- MVP 패턴에 대한 자세한 설명: <https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93presenter>
- Flutter 예제 코드: <https://github.com/flutter/flutter>