# Provider状态管理

Provider 是 Flutter 中最受欢迎的状态管理解决方案之一，它是对 InheritedWidget 的封装，使得状态管理更加简单和高效。本教程将带你全面了解 Provider 的使用方法。


## 相关依赖
```yaml
dependencies:
  flutter:
    sdk: flutter
  provider: ^6.1.5
```
执行命令：`flutter pub get`

或者执行安装命令：`flutter pub add provider`

## 基础使用

### 1.创建基础Model

```dart
class Counter with ChangeNotifier {
  int _count = 0;
  
  int get count => _count;
  
  void increment() {
    _count++;
    notifyListeners(); // 通知监听者数据已变化
  }
}
```

### 2.在顶层提供Model

```dart
void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => Counter(),
      child: MyApp(),
    ),
  );
}
```

### 3.在子Widget中访问Model


```dart
class CounterDisplay extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Text(
      'Count: ${context.watch<Counter>().count}',
      style: Theme.of(context).textTheme.headline4,
    );
  }
}

class IncrementButton extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: () => context.read<Counter>().increment(),
      child: Text('Increment'),
    );
  }
}
```

## Provider类别

### Provider
最基本的 provider，用于提供不可变值。

```dart
Provider<String>(
  create: (context) => 'Hello, Provider!',
  child: ...
);
```

### ChangeNotifierProvider
用于提供可监听变化的对象。

```dart
ChangeNotifierProvider(
  create: (context) => MyModel(),
  child: ...
);
```

### FutureProvider
用于提供异步数据。


```dart
FutureProvider<User>(
  create: (context) => fetchUser(),
  initialData: User.empty(),
  child: ...
);
```

### StreamProvider
用于提供流数据。

```dart
StreamProvider<int>(
  create: (context) => streamOfInts(),
  initialData: 0,
  child: ...
);
```

### MultiProvider
当需要提供多个 provider 时使用。

```dart
MultiProvider(
  providers: [
    Provider<Something>(create: (_) => Something()),
    Provider<SomethingElse>(create: (_) => SomethingElse()),
    Provider<AnotherThing>(create: (_) => AnotherThing()),
  ],
  child: ...
)
```

## Consumer与Selector

### Consumer
当只需要 widget 树的一部分访问 provider 时使用
```dart
Consumer<Counter>(
  builder: (context, counter, child) {
    return Text('${counter.count}');
  },
)
```

### Selector
当只需要监听 model 的特定部分变化时使用，可以优化性能。

```dart
Selector<Counter, int>(
  selector: (context, counter) => counter.count,
  builder: (context, count, child) {
    return Text('$count');
  },
)
```


## ProxyProvider
ProxyProvider 是 Provider 包中用于处理依赖关系的特殊 provider，它允许一个 provider 依赖于另一个 provider 的值。

### 基础语法
```dart
ProxyProvider<Dependency, Result>(
  create: (context) => Result(), // 可选，用于初始创建
  update: (context, dependency, previous) => Result(dependency),
  dispose: (context, value) => value.dispose(), // 可选
  child: childWidget,
)
```
create: 初始创建函数（可选）

update: 更新函数（必需）

dispose: 清理函数（可选）

child: 子 widget

```dart
// 认证服务
class AuthService {
  String? _token;

  String? get token => _token;

  void login(String user, String pass) {
    _token = 'generated_token_for_$user';
  }
}

// 用户信息服务（依赖认证token）
class UserInfo {
  final String? token;
  final String data;

  UserInfo(this.token) : data = token != null ? 'User data for $token' : 'No user';
}

// 在widget树顶部设置
void main() {
  runApp(
    MultiProvider(
      providers: [
        Provider(create: (_) => AuthService()),
        ProxyProvider<AuthService, UserInfo>(
          update: (_, auth, __) => UserInfo(auth.token),
        ),
      ],
      child: MyApp(),
    ),
  );
}
```


## 完整事例

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(
    MultiProvider(
      providers: [
        ChangeNotifierProvider(create: (_) => Counter()),
        Provider(create: (_) => SomeOtherClass()),
      ],
      child: MyApp(),
    ),
  );
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Provider Demo')),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              Text('You have pushed the button this many times:'),
              Consumer<Counter>(
                builder: (context, counter, child) => Text(
                  '${counter.count}',
                  style: Theme.of(context).textTheme.headline4,
                ),
              ),
              IncrementButton(),
            ],
          ),
        ),
      ),
    );
  }
}

class Counter with ChangeNotifier {
  int _count = 0;

  int get count => _count;

  void increment() {
    _count++;
    notifyListeners();
  }
}

class IncrementButton extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: () => context.read<Counter>().increment(),
      child: Text('Increment'),
    );
  }
}

class SomeOtherClass {}
```
