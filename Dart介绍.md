# Dart介绍

## Dart特点

Dart是面向对象开发语言,所有都是对象,所有对象的基类为Object,

Dart是强类型语言,不过可以使用var声明变量,因为Dart可以进行类型推断,

Dart支持顶级函数,函数在Dart也是对象

Dart支持顶级变量

Dart中没有关键字public、protected和private。如想设置私有变量或函数，则变量和函数名以下划线（_）开头。

## 变量

### 变量的声明
声明变量方式:
```dart
var name = 'Box';
String name1 = 'Lili';
```

这个类型之后不能再改变,如果想要改变,可以使用dynamic类型,

```dart
dynamic name = 'Bob';
```

### 默认值
所有对象的默认都是null,


### final和const

如果不打算更改变量，可以使用final或者const。一个final变量只能被设置一次，而const变量是编译时常量，定义时必须赋值。


### 内置类型

Dart语言支持以下类型:
- numbers  
    包含int和double
    ```dart
    var y = 1.1;
    var exponents = 1.42e5;
    double z = 1; // Equivalent to double z = 1.0.
    ```
- strings  
    单引号双引号都可以,插入表达式使用`$(exp)`,多行文本使用三个引号
- booleans  
    bool类型,只有两个都是bool类型的对象才能够做比较
- lists  
    dart中的数组是Lists对象
    ```dart
    var list = [1, 2, 3];
    ```
- sets
    set保存没有重复元素的集合
    ```dart
    var halogens = {'fluorine', 'chlorine', 'bromine', 'iodine', 'astatine'};
    ```
- maps
    ```dart
    var gifts = {
  // Key:    Value
  'first': 'partridge',
  'second': 'turtledoves',
  'fifth': 'golden rings'
    };

    var nobleGases = {
     2: 'helium',
     10: 'neon',
     18: 'argon',
    };
    ```

