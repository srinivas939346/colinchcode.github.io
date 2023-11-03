---
layout: post
title: "[flutter] 플러터(Flutter)에서 통합 테스트(Integration Test) 작성하기"
description: " "
date: 2023-11-03
tags: [flutter]
comments: true
share: true
---

플러터(Flutter)는 Google이 개발한 모바일 앱 개발 프레임워크로, 다양한 플랫폼에서 동작하는 애플리케이션을 작성할 수 있습니다. 앱의 품질을 보장하기 위해 통합 테스트(Integration Test)를 작성하는 것은 매우 중요합니다. 이번 글에서는 플러터에서 통합 테스트를 작성하는 방법에 대해 알아보겠습니다.

## 1. 통합 테스트란?

통합 테스트는 애플리케이션의 여러 구성 요소들이 함께 작동하는지 확인하는 테스트입니다. 이는 사용자 경험을 향상시키고, 예기치 않은 버그를 방지하는 데 도움이 됩니다. 플러터에서는 통합 테스트를 작성하기 위해 `flutter_driver` 패키지를 사용합니다.

## 2. `flutter_driver` 패키지 설치하기

`flutter_driver` 패키지를 사용하기 위해 프로젝트의 `pubspec.yaml` 파일에 아래와 같이 의존성을 추가하세요.

```yaml
dev_dependencies:
  flutter_driver:
    sdk: flutter
```

의존성을 추가한 후 터미널에서 `flutter packages get` 명령어를 사용하여 패키지를 다운로드합니다.

## 3. 통합 테스트 작성하기

통합 테스트를 작성하기 위해서는 `test_driver` 폴더에 `app.dart` 파일을 생성해야 합니다. 아래는 `app.dart` 파일의 예시 코드입니다.

```dart
import 'package:flutter_driver/driver_extension.dart';
import 'package:your_app/main.dart' as app;

void main() {
  // 테스트 확장을 사용하여 앱을 테스트 모드로 실행합니다.
  enableFlutterDriverExtension();

  // 앱을 실행시킵니다.
  app.main();
}
```

이제 위에서 작성한 `app.dart` 파일을 사용하여 앱을 테스트할 수 있습니다. 터미널에서 아래의 명령어를 실행하여 테스트를 시작하세요.

```shell
flutter drive --target=test_driver/app.dart
```

## 4. 통합 테스트 작성하기

실제로 테스트를 작성해보겠습니다. `test_driver` 폴더에 `app_test.dart` 파일을 생성하고, 아래의 코드를 추가합니다.

```dart
import 'package:flutter_driver/flutter_driver.dart';
import 'package:test/test.dart';

void main() {
  FlutterDriver driver;

  // 테스트 전에 앱을 실행합니다.
  setUpAll(() async {
    driver = await FlutterDriver.connect();
  });

  // 테스트 후에 앱을 종료합니다.
  tearDownAll(() async {
    if (driver != null) {
      driver.close();
    }
  });

  // 예제 테스트 케이스
  test('테스트 예시', () async {
    // 여기에 테스트 코드를 작성합니다.
    // 예를 들어, 화면의 위젯을 찾아 테스트를 진행할 수 있습니다.
    final buttonFinder = find.byValueKey('my_button');
    expect(await driver.getText(buttonFinder), '버튼');

    // 테스트를 위해 액션을 수행하고 결과를 확인할 수 있습니다.
    await driver.tap(buttonFinder);
    expect(await driver.getText(buttonFinder), '클릭됨');
  });
}
```

위의 코드는 간단한 예시 테스트 케이스입니다. `setUpAll` 메서드를 사용하여 테스트 전에 앱을 실행하고, `tearDownAll` 메서드를 사용하여 테스트 후에 앱을 종료합니다. `test` 메서드 내에서 원하는 테스트 코드를 작성하면 됩니다.

## 5. 테스트 실행하기

위의 `app.dart` 파일을 실행하는 방법과 같이 `app_test.dart` 파일을 실행하면 통합 테스트가 실행됩니다.

```shell
flutter drive --target=test_driver/app_test.dart
```

테스트가 성공적으로 완료된 후에는 터미널에서 결과를 확인할 수 있습니다.

## 참고 자료

- [Flutter 통합 테스트 문서](https://flutter.dev/docs/testing/integration-tests)
- [flutter_driver 패키지](https://pub.dev/packages/flutter_driver)

통합 테스트를 작성하여 플러터 애플리케이션의 안정성과 품질을 보장할 수 있습니다. 테스트 코드를 작성하고 실행해보면서 앱의 기능을 효과적으로 검증해보세요!