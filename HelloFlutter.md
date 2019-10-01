# 第一个Flutter项目

## 环境检查

确保Flutter SDK安装成功并配置了正确的环境变量   
使用flutter doctor检查通过  
确保连接了至少一个设备

## 新建项目

在IDE中点击“New Flutter Project”。
在lib/main.dart中放入代码。
```Dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Welcome to Flutter',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Welcome to Flutter'),
        ),
        body: Center(
          child: Text('Hello World'),
        ),
      ),
    );
  }
}
```

## 运行

点击运行 或 在项目根目录的命令行中运行flutter run