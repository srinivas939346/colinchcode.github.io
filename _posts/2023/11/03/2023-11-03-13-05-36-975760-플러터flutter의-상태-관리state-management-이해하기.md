---
layout: post
title: "[flutter] 플러터(Flutter)의 상태 관리(State Management) 이해하기"
description: " "
date: 2023-11-03
tags: [flutter]
comments: true
share: true
---

안녕하세요! 이번에는 플러터(Flutter)의 상태 관리(State Management)에 대해 알아보겠습니다. 플러터는 싱글 페이지 애플리케이션 프레임워크로서, 사용자 인터페이스(UI)를 빠르게 개발할 수 있도록 도와줍니다. 하지만 애플리케이션의 복잡성이 증가하면서 상태 관리는 중요한 이슈가 되었습니다.

## 상태 관리(State Management)란 무엇인가요?

상태 관리는 애플리케이션의 데이터(상태)를 관리하고, 이를 사용자 인터페이스와 동기화하는 과정을 의미합니다. 플러터에서의 상태 관리는 애플리케이션의 화면이 변하는 동안 데이터의 상태를 유지하는 것을 의미합니다. 상태 관리를 올바르게 구현하면 애플리케이션의 성능과 사용자 경험을 향상시킬 수 있습니다.

## 왜 상태 관리가 필요한가요?

애플리케이션은 다양한 상태를 가질 수 있습니다. 사용자가 입력한 데이터, 네트워크 요청 결과, 앱 내부에서 생성되는 데이터와 같이 상태는 동적으로 변할 수 있습니다. 이러한 동적인 상태를 효율적으로 관리하기 위해 상태 관리는 필수적입니다. 또한 플러터는 위젯 트리의 모든 위젯이 상태가 있는 위젯이기 때문에, 상태 관리는 플러터 앱 개발에 더욱 중요한 역할을 합니다.

## 플러터에서의 상태 관리 방법

플러터에서는 다양한 상태 관리 방법을 활용할 수 있습니다. 대표적인 방법으로는 `setState` 메소드, `Provider`, `Bloc`, `MobX` 등이 있습니다. 

### 1. setState 메소드

`setState` 메소드는 가장 기본적인 상태 관리 방법입니다. 위젯의 상태가 변경될 때마다 호출하여 화면을 다시 그립니다. 간단한 애플리케이션의 경우에는 충분히 사용할 수 있지만, 복잡한 상태 관리에는 유지보수 및 성능 문제가 발생할 수 있습니다.

```dart
class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
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
        title: Text('State Management with setState'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.headline4,
            ),
            RaisedButton(
              onPressed: _incrementCounter,
              child: Text('Increment'),
            ),
          ],
        ),
      ),
    );
  }
}
```

### 2. Provider

Provider는 플러터 커뮤니티에서 많이 사용되는 상태 관리 패키지입니다. Provider는 동작 방식과 사용법이 간단하며, 의존성 주입(Dependency Injection)과 같은 기능을 제공합니다.

```dart
class Counter with ChangeNotifier {
  int _count = 0;

  int get count => _count;

  void increment() {
    _count++;
    notifyListeners();
  }
}

class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (context) => Counter(),
      child: Scaffold(
        appBar: AppBar(
          title: Text('State Management with Provider'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              Consumer<Counter>(
                builder: (context, counter, child) {
                  return Text(
                    '${counter.count}',
                    style: Theme.of(context).textTheme.headline4,
                  );
                },
              ),
              RaisedButton(
                onPressed: () {
                  Provider.of<Counter>(context, listen: false).increment();
                },
                child: Text('Increment'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

### 3. Bloc

Bloc(Business Logic Component)은 상태 관리를 위한 또 다른 방법입니다. Bloc 패턴은 사용자 인터페이스와 비즈니스 로직을 분리하여 앱의 복잡성을 관리하고, 테스트 및 재사용성을 높일 수 있는 패턴입니다.

```dart
class CounterBloc extends Bloc<CounterEvent, int> {
  @override
  int get initialState => 0;

  @override
  Stream<int> mapEventToState(CounterEvent event) async* {
    if (event is IncrementEvent) {
      yield state + 1;
    }
  }
}

class CounterEvent {}

class IncrementEvent extends CounterEvent {}

class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return BlocProvider<CounterBloc>(
      create: (context) => CounterBloc(),
      child: Scaffold(
        appBar: AppBar(
          title: Text('State Management with Bloc'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              BlocBuilder<CounterBloc, int>(
                builder: (context, count) {
                  return Text(
                    '$count',
                    style: Theme.of(context).textTheme.headline4,
                  );
                },
              ),
              RaisedButton(
                onPressed: () {
                  BlocProvider.of<CounterBloc>(context).add(IncrementEvent());
                },
                child: Text('Increment'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

## 결론

상태 관리는 플러터 앱 개발에서 매우 중요한 요소입니다. 위에서 소개한 setState, Provider, Bloc은 플러터 앱의 상태 관리를 위해 자주 사용되는 방법입니다. 애플리케이션의 규모와 요구 사항에 맞게 상태 관리 방법을 선택하고, 효율적으로 사용하여 플러터 앱을 개발해보세요. 

더 자세한 내용은 아래 참고 자료를 확인하시기 바랍니다.

- [Flutter 공식 문서](https://flutter.dev/docs/development/data-and-backend/state-mgmt)
- [Flutter Provider 패키지](https://pub.dev/packages/provider)
- [Flutter Bloc 패키지](https://pub.dev/packages/flutter_bloc)

감사합니다!