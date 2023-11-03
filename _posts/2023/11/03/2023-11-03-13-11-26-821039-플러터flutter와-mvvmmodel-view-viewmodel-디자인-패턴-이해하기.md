---
layout: post
title: "[flutter] 플러터(Flutter)와 MVVM(Model-View-ViewModel) 디자인 패턴 이해하기"
description: " "
date: 2023-11-03
tags: [flutter]
comments: true
share: true
---

플러터(Flutter)는 Google에서 개발한 UI 프레임워크로, iOS와 Android 모두에서 동일한 코드로 앱을 개발할 수 있는 장점이 있습니다. 

MVVM(Model-View-ViewModel)은 앱의 UI 로직과 비즈니스 로직을 분리하기 위한 디자인 패턴입니다. 앱의 데이터를 관리하고 화면 갱신을 처리하는 ViewModel 레이어를 중심으로 구성되어 있습니다.

### MVVM 구성 요소

1. Model: 앱의 데이터를 나타내는 부분입니다. 주로 데이터 모델 클래스로 구현되며, ViewModel과의 데이터 바인딩을 통해 상호작용합니다.

2. View: 앱의 화면을 렌더링하는 부분입니다. Widget으로 구성되어 있으며, ViewModel과의 데이터 바인딩을 통해 상태를 표현하고 갱신합니다.

3. ViewModel: View와 Model 사이의 다리 역할을 합니다. 비즈니스 로직을 처리하고, Model에서 가져온 데이터를 가공한 뒤 View에게 전달해주는 역할을 합니다.

### 플러터(Flutter)에서의 MVVM 적용

Flutter에서는 Provider 패키지를 사용하여 MVVM 패턴을 구현할 수 있습니다. Provider는 상태 관리를 위한 라이브러리로, ViewModel을 만들어 상태를 관리하고 이를 View와 바인딩할 수 있습니다.

#### 예제 코드

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

class User {
  String name;
  int age;

  User({required this.name, required this.age});
}

class UserViewModel extends ChangeNotifier {
  User _user = User(name: 'John Doe', age: 25);

  User get user => _user;

  void updateUser(String name, int age) {
    _user.name = name;
    _user.age = age;
    notifyListeners();
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('User Profile'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'Name: ${Provider.of<UserViewModel>(context).user.name}',
              style: TextStyle(fontSize: 18),
            ),
            Text(
              'Age: ${Provider.of<UserViewModel>(context).user.age}',
              style: TextStyle(fontSize: 18),
            ),
            ElevatedButton(
              onPressed: () => Navigator.push(
                context,
                MaterialPageRoute(builder: (_) => EditProfilePage()),
              ),
              child: Text('Edit Profile'),
            ),
          ],
        ),
      ),
    );
  }
}

class EditProfilePage extends StatefulWidget {
  @override
  _EditProfilePageState createState() => _EditProfilePageState();
}

class _EditProfilePageState extends State<EditProfilePage> {
  late TextEditingController _nameController;
  late TextEditingController _ageController;

  @override
  void initState() {
    super.initState();
    final userViewModel = Provider.of<UserViewModel>(context, listen: false);
    _nameController = TextEditingController(text: userViewModel.user.name);
    _ageController = TextEditingController(text: userViewModel.user.age.toString());
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Edit Profile'),
      ),
      body: Container(
        padding: EdgeInsets.all(20),
        child: Column(
          children: <Widget>[
            TextField(
              controller: _nameController,
              decoration: InputDecoration(labelText: 'Name'),
            ),
            TextField(
              controller: _ageController,
              decoration: InputDecoration(labelText: 'Age'),
            ),
            ElevatedButton(
              onPressed: () {
                final userViewModel = Provider.of<UserViewModel>(context, listen: false);
                userViewModel.updateUser(_nameController.text, int.parse(_ageController.text));
                Navigator.pop(context);
              },
              child: Text('Save'),
            ),
          ],
        ),
      ),
    );
  }
}

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => UserViewModel(),
      child: MaterialApp(
        home: HomePage(),
      ),
    ),
  );
}
```

위의 예제 코드는 간단한 사용자 프로필 앱을 구현한 것입니다. User 객체와 UserViewModel 클래스를 정의하고, HomePage와 EditProfilePage에서 Provider 패키지를 사용하여 ViewModel과 View를 바인딩합니다. 

UserViewModel 클래스에서는 User 객체를 관리하고, updateUser 함수를 통해 사용자 정보를 업데이트하고 View에게 알립니다. 이를 통해 데이터의 일관성과 화면 갱신이 원활하게 이루어집니다.

플러터(Flutter)의 Provider 패키지를 사용하면 MVVM 디자인 패턴을 쉽게 구현할 수 있으며, 이를 통해 앱의 유지 보수성과 확장성을 높일 수 있습니다.

### 참고 자료

- [Flutter 공식 문서](https://flutter.dev/docs)
- [Provider 패키지 GitHub](https://github.com/rrousselGit/provider)