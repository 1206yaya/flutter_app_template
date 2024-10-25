# Examples app of Flutter App Template

## Flavor with App ID

- dev: com.u1206yaya.FlutterAppTemplate.dev
- stg: com.u1206yaya.FlutterAppTemplate.stg
- prod: com.u1206yaya.FlutterAppTemplate

## Features

- Riverpod examples
- Theme selector

## App settings

| Category                                 | Description                | Codes                                            |
| ---------------------------------------- | -------------------------- | ------------------------------------------------ |
| [FVM](https://github.com/leoafarias/fvm) | Flutter Version Management | [.fvmrc](../../.fvmrc)                           |
| Dart                                     | Dart version               | [pubspec.yaml](./pubspec.yaml)                   |
| Dart                                     | Lint / Analyze             | [analysis_options.yaml](./analysis_options.yaml) |

## Dependency Packages

### State Management

- [Riverpod](https://riverpod.dev/)

### Code Generation

- [freezed](https://pub.dev/packages/freezed)
- [json_serializable](https://pub.dev/packages/json_serializable)

### Hooks

- [Flutter Hooks](https://pub.dev/packages/flutter_hooks)

### Router

- [go_router](https://pub.dev/packages/go_router)

## App structure

- lib/
  - commons/
  - features/
  - presentation/
  - main.dart

## Secret files required for Release

Required only `--release` mode.

- android/key.properties
- android/app/upload-keystore.jks

The jks file was converted to Base64 and registered as Secret because it is used by Continuous Delivery.

```
base64 --input upload-keystore.jks | pbcopy
```

## How to use

### Localizations

Create JSON files.

```json
{
  "hello": "Hello $name",
  "save": "Save",
  "login": {
    "success": "Logged in successfully",
    "fail": "Logged in failed"
  }
}
```

Generate Dart files.

```shell
dart run slang
```

Use the generated file.

```dart
import '../../../gen/strings.g.dart';

final t = Translations.of(context);
```

## FlutterFire Configure

When should it be re-run?

- Add support for new platforms
- Start using new Firebase services and products

```shell
# Dev
flutterfire configure --yes \
--project flutter-app-template-dev \
--out lib/environment/src/firebase_options_dev.dart \
--platforms android,ios,macos,web \
--android-package-name com.u1206yaya.FlutterAppTemplate.dev \
--ios-bundle-id com.u1206yaya.FlutterAppTemplate.dev \
--macos-bundle-id com.u1206yaya.FlutterAppTemplate.dev

# Stg
flutterfire configure --yes \
--project flutter-app-template-stg \
--out lib/environment/src/firebase_options_stg.dart \
--platforms android,ios,macos,web \
--android-package-name com.u1206yaya.FlutterAppTemplate.stg \
--ios-bundle-id com.u1206yaya.FlutterAppTemplate.stg \
--macos-bundle-id com.u1206yaya.FlutterAppTemplate.stg

# Prod
flutterfire configure --yes \
--project altive-fat \
--out lib/environment/src/firebase_options_prod.dart \
--platforms android,ios,macos,web \
--android-package-name com.u1206yaya.FlutterAppTemplate \
--ios-bundle-id com.u1206yaya.FlutterAppTemplate \
--macos-bundle-id com.u1206yaya.FlutterAppTemplate
```

### Firebase Analytics DebugView

#### Start/Stop DebugView for Android

```shell
# Start
adb shell setprop debug.firebase.analytics.app com.u1206yaya.FlutterAppTemplate.dev
# Stop
adb shell setprop debug.firebase.analytics.app .none.
```
