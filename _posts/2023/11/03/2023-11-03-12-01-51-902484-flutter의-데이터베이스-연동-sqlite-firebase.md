---
layout: post
title: "[flutter] Flutter의 데이터베이스 연동 (SQLite, Firebase)"
description: " "
date: 2023-11-03
tags: [flutter]
comments: true
share: true
---

Flutter는 모바일 애플리케이션 개발을 위한 매우 강력한 프레임워크입니다. 데이터베이스는 대부분의 앱에서 필수적인 요소이며, Flutter에서는 SQLite와 Firebase를 사용하여 데이터베이스를 연동할 수 있습니다. 이번 포스트에서는 Flutter 앱에서 SQLite와 Firebase 데이터베이스를 연동하는 방법에 대해 알아보겠습니다.

## SQLite 데이터베이스 연동

SQLite는 경량의 오픈소스 RDBMS(Relational Database Management System)로, 작은 크기의 데이터베이스를 지원하고 로컬 저장소에 데이터를 저장할 수 있습니다. Flutter에서는 `sqflite` 패키지를 사용하여 SQLite 데이터베이스를 연동할 수 있습니다.

### 1. 패키지 추가하기

먼저, `sqflite` 패키지를 프로젝트에 추가해야 합니다. `pubspec.yaml` 파일에 다음 코드를 추가합니다.

```yaml
dependencies:
  sqflite: ^2.0.0
  path_provider: ^2.0.2
```

### 2. 데이터베이스 생성하기

SQLite 데이터베이스를 생성하기 위해 `Database` 클래스를 사용합니다. 다음은 데이터베이스 생성과 테이블 생성하는 예제 코드입니다.

```dart
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

void main() async {
  final database = openDatabase(
    join(await getDatabasesPath(), 'my_database.db'),
    onCreate: (db, version) {
      return db.execute(
        'CREATE TABLE my_table(id INTEGER PRIMARY KEY, name TEXT)',
      );
    },
    version: 1,
  );
}
```

### 3. 데이터 추가/조회/수정/삭제하기

데이터베이스에 데이터를 추가, 조회, 수정, 삭제하기 위해서는 `Database` 클래스의 메서드를 사용합니다. 다음은 데이터를 추가하고 조회하는 예제 코드입니다.

```dart
void main() async {
  final database = await openDatabase(...);

  await database.insert(
    'my_table',
    {
      'id': 1,
      'name': 'John',
    },
    conflictAlgorithm: ConflictAlgorithm.replace,
  );

  final List<Map<String, dynamic>> maps = await database.query('my_table');

  print(maps);
}
```

위의 코드에서 `insert` 메서드를 사용하여 데이터를 추가하고, `query` 메서드를 사용하여 테이블의 모든 데이터를 조회하고 있습니다.

## Firebase 데이터베이스 연동

Firebase는 Google에서 제공하는 모바일 및 웹 애플리케이션 개발 플랫폼입니다. Flutter에서는 Firebase를 사용하여 실시간 데이터베이스를 구축할 수 있습니다.

### 1. 프로젝트 설정하기

Firebase 프로젝트를 설정하고, Firebase Console에서 실시간 데이터베이스를 생성해야 합니다. Firebase Console에서 데이터베이스 규칙을 설정하고, 데이터를 관리할 수 있습니다.

### 2. Firebase SDK 추가하기

Flutter 프로젝트에 Firebase SDK를 추가하여 Firebase와 연동해야 합니다. [FlutterFire](https://firebase.flutter.dev/)를 사용하면 간편하게 Firebase SDK를 가져올 수 있습니다.

### 3. 데이터 추가/조회/수정/삭제하기

Firebase 실시간 데이터베이스를 사용하여 데이터를 추가, 조회, 수정, 삭제할 수 있습니다. 예를 들어, 다음과 같이 데이터를 추가하고 조회하는 코드를 작성할 수 있습니다.

```dart
import 'package:firebase_database/firebase_database.dart';

void main() {
  final database = FirebaseDatabase.instance.reference();

  database.child('users').push().set({
    'id': 1,
    'name': 'John',
  });

  database.child('users').once().then((DataSnapshot snapshot) {
    print(snapshot.value);
  });
}
```

위의 코드에서 `push` 메서드를 사용하여 데이터를 추가하고, `once` 메서드를 사용하여 데이터를 조회하고 있습니다.

## 결론

Flutter에서 데이터베이스를 연동하는 방법에 대해 알아보았습니다. SQLite와 Firebase는 각각 로컬 저장소와 실시간 데이터베이스를 지원하며, 데이터의 처리와 관리를 용이하게 해줍니다. 앱의 특성과 요구사항에 맞게 데이터베이스를 선택하여 Flutter 앱을 개발해 보시기 바랍니다.

### 참고 자료

- [sqflite - Flutter packages](https://pub.dev/packages/sqflite)
- [path_provider - Flutter packages](https://pub.dev/packages/path_provider)
- [Firebase 실시간 데이터베이스 사용하기 - Flutter](https://firebase.flutter.dev/docs/database/overview)
- [Firebase Console](https://console.firebase.google.com/)