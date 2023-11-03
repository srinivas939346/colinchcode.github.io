---
layout: post
title: "[flutter] 플러터(Flutter)의 상태 관리(State Management) 방법 소개"
description: " "
date: 2023-11-03
tags: [flutter]
comments: true
share: true
---

플러터(Flutter)는 Google에서 개발한 모바일 애플리케이션 프레임워크로, 다양한 플랫폼에서 동작하는 네이티브 수준의 앱을 만들 수 있습니다. 플러터의 가장 큰 특징 중 하나는 상태 관리(State Management)의 유연성입니다. 이 글에서는 플러터의 상태 관리 방법을 소개하고, 어떤 상황에 어떤 방법을 사용해야 하는지 알아보겠습니다.

## 1. 상태 관리란?

상태 관리는 애플리케이션에서 데이터의 변경 사항을 추적하고, 해당 변경 사항에 따라 화면을 업데이트하는 것을 의미합니다. 플러터에서는 화면을 업데이트하기 위해 상태 관리가 필요한데, 이는 사용자 입력, 네트워크 상태, 데이터 소스 변경 등 다양한 요소와 상호 작용하기 때문입니다.

## 2. 플러터의 상태 관리 방법

### 2.1. 상태 관리 없이 UI 업데이트하기

가장 간단한 방법은 상태 관리 없이 UI를 업데이트하는 것입니다. 이 방법은 단순한 앱이나 작은 규모의 앱에서는 괜찮지만, 복잡한 앱에서는 복잡성과 유지 보수성 문제가 발생할 수 있습니다.

```dart
class MyHomePage extends StatelessWidget {
  int _counter = 0;

  void _incrementCounter() {
    _counter++;
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('My App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text('Counter: $_counter'),
            RaisedButton(
              child: Text('Increment'),
              onPressed: _incrementCounter,
            ),
          ],
        ),
      ),
    );
  }
}
```

### 2.2. StatefulWidget을 사용한 간단한 상태 관리

다음으로는 StatefulWidget을 사용하여 간단한 상태 관리를 할 수 있습니다. StatelessWidget과는 달리 StatefulWidget은 변경 가능한 상태를 가질 수 있습니다. 해당 상태가 변경되면 Flutter는 자동으로 UI를 업데이트합니다.

```dart
class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('My App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text('Counter: $_counter'),
            RaisedButton(
              child: Text('Increment'),
              onPressed: _incrementCounter,
            ),
          ],
        ),
      ),
    );
  }
}
```

### 2.3. Provider 패키지를 사용한 상태 관리

더 복잡한 앱에서는 Provider 패키지를 사용하는 것이 좋습니다. Provider는 의존성 주입(Dependency Injection)과 통합되어 복잡한 상태 관리를 간단하게 만들어 줍니다. 이를 통해 상태 변경을 구독하고, 필요한 곳에서 상태를 사용할 수 있습니다. Provider 패키지는 다음과 같이 사용할 수 있습니다.

```dart
class Counter with ChangeNotifier {
  int _count = 0;

  int get count => _count;

  void increment() {
    _count++;
    notifyListeners();
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final counter = Provider.of<Counter>(context);

    return Scaffold(
      appBar: AppBar(
        title: Text('My App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text('Counter: ${counter.count}'),
            RaisedButton(
              child: Text('Increment'),
              onPressed: () => counter.increment(),
            ),
          ],
        ),
      ),
    );
  }
}
```

## 3. 어떤 방법을 사용해야 할까요?

플러터에서 상태 관리를 위해 선택할 수 있는 다양한 방법이 있습니다. 작은 규모의 앱이라면 상태 관리 없이 UI를 업데이트하는 방법도 충분히 사용할 수 있습니다. 하지만 중대형 앱이나 복잡한 상태 관리가 필요한 경우, StatefulWidget이나 Provider 패키지를 사용하는 것을 권장합니다. StatefulWidget은 간단한 앱에서 사용하기 적합하며, Provider 패키지는 의존성 주입과 통합하여 더 복잡한 상태 관리를 할 때 사용하면 좋습니다.

## 참고 자료
- [Flutter 공식 문서](https://flutter.dev/)
- [Provider 패키지 GitHub 레포지토리](https://github.com/rrousselGit/provider)