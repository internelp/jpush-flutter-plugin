[![QQ Group](https://img.shields.io/badge/QQ%20Group-862401307-red.svg)]()
# JPush Flutter Plugin

### 安装

在工程 pubspec.yaml 中加入 dependencies

```yaml
dependencies:
  jpush_flutter: 0.0.11
```

### 配置

##### Android:

在 `/android/app/build.gradle` 中添加下列代码：

```groovy
android: {
  ....
  defaultConfig {
    applicationId "替换成自己应用 ID"
    ...
    ndk {
	//选择要添加的对应 cpu 类型的 .so 库。
	abiFilters 'armeabi', 'armeabi-v7a', 'x86', 'x86_64', 'mips', 'mips64', 'arm64-v8a',        
    }

    manifestPlaceholders = [
        JPUSH_PKGNAME : applicationId,
        JPUSH_APPKEY : "appkey", // NOTE: JPush 上注册的包名对应的 Appkey.
        JPUSH_CHANNEL : "developer-default", //暂时填写默认值即可.
    ]
  }    
}
```

##### iOS:

- 在 xcode8 之后需要点开推送选项： TARGETS -> Capabilities -> Push Notification 设为 on 状态

### 使用

```dart
import 'package:jpush_flutter/jpush_flutter.dart';
```

### APIs

**注意** : 需要先调用 JPush.setup 来初始化插件，才能保证其他功能正常工作。

 [参考](./documents/APIs.md)

### Fork 后新增功能

获取 `device token` 后存到本地，可以用下面方法取出，然后自行通过 APNs 发送消息。

在工程 pubspec.yaml 中替换 dependencies：
```yaml
dependencies:
  jpush_flutter: 
    git: https://github.com/internelp/jpush-flutter-plugin
```

使用 jpush 注册 push 权限后，可以从程序中取出 device token 使用，此时既可以使用 jpush，也可以直接使用 APNs：
```dart
import 'package:shared_preferences/shared_preferences.dart';

SharedPreferences prefs = await SharedPreferences.getInstance();
var _deviceToken = prefs.getString("deviceToken");
deviceToken = _deviceToken;
```
