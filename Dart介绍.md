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

## 运算符  

除了和Java中常见运算符,还有几个特别说明的运算法:

- ?.  
判空调用运算法  

```dart
//定义类
class Person {
  var name;
  Person(this.name);
}

// 调用
Person p;
var name = p?.name; //先判断p是否为null，如果是，则name为null；如果否，则返回p.name值
print("name = $name");

// 输出结果
name = null
```

- ~/  
```dart
// 代码语句
var num = 10;
var result = num ~/ 3; //得出一个小于等于(num/3)的最大整数
print("result = $result");

// 输出结果
result = 3
```

- as  
进行类型转化  
```dart 
// 类定义
class Banana {
  var weight;
  Banana(this.weight);
}

class Apple {
  var weight;
  Apple(this.weight);
}

// 调用
dynamic b = Banana(20);
(b as Banana).weight = 20; // 正常执行
print("b.weight = ${(b as Banana).weight}");
(b as Apple).weight = 30; // 类型转换错误，运行报错
print("b.weight = ${(b as	Apple).weight}");

//输出结果
b.weight = 20
Uncaught exception:
CastError: Instance of 'Banana': type 'Banana' is not a subtype of type 'Apple'
```

- is  
类似Java中的instanceof  
```dart
// 函数和类代码定义
getFruit() => Banana(20); // 获取一个水果对象

class Banana {
  var weight;
  Banana(this.weight);
}

class Apple {
  var color;
  Apple(this.color);
}

// 调用
var b = getFruit();
if(b is Apple) { //判断对象是否为Apple类
  print("The fruit is an apple");
} else if(b is Banana) { //判断水果是否为Banana类
  print("The fruit is a banana");
}

// 输出结果
The fruit is a banana
```

- ??  
判空操作  
```dart
// 操作代码块
String name;
String nickName = name ?? "Nick"; //如果name不为null，则nickName值为name的值，否则值为Nick
print("nickName = $nickName");
  
name = "Bruce";
nickName = name ?? "Nick"; //如果name不为null，则nickName值为name的值，否则值为Nick
print("nickName = $nickName");
  
// 输出结果
nickName = Nick
nickName = Bruce 
```

- ..   
级联操作允许对同一个对象进行一系列操作  

```dart
// 类定义
class Banana {
  var weight;
  var color;
  Banana(this.weight, this.color);
  
  void showWeight() {
    print("weight = $weight");
  }
  
  void showColor() {
    print("color = $color");
  }
}

// 调用
Banana(20, 'yellow')
    ..showWeight()
    ..showColor();
    
// 输出结果
weight = 20
color = yellow
```

## 控制语句  

Dart重的控制语句和Java中基本相同

- 特殊说明`switch-case`,可以使用continue语句和标签来执行指定case语句。
    ```dart
    var fruit = 'apple';
    switch (fruit) {
      case 'banana':
        print("this is a banana");
        continue anotherFruit;

      anotherFruit:
      case 'apple':
        print("this is an apple");
        break;
    }

    // 输出结果
    this is an apple
    ```

## 函数

Dart是一种真正的面向对象语言，因此即使是函数也是对象并且具有类型Function。这意味着函数可以分配给变量或作为参数传递给其他函数。

```dart
String getName() {
  return "Bruce";
}

// 如果函数体中只包含一个表达式，则可以使用简写语法
String getName() => "Bruce";
```

### 参数说明

- 可选参数  
    Dart函数可以设置可选参数，可以使用命名参数也可以使用位置参数。
    ```dart
    // 函数定义
    void showDesc({var name, var age}) {
      if(name != null) {
        print("name = $name");
      }
      if(age != null) {
        print("age = $age");
      }
    }
    // 函数调用
    showDesc(name: "Bruce");
    // 输出结果
    name = Bruce
    ```
- 位置参数  
    使用 [] 来标记可选参数
    ```dart
    // 函数定义
    void showDesc(var name, [var age]) {
      print("name = $name");
    
      if(age != null) {
        print("age = $age");
      }
    }

    // 函数调用
    showDesc("Bruce");

    // 输出结果
    name = Bruce
    ```
- 默认值
    ```dart
    // 函数定义
    void showDesc(var name, [var age = 18]) {
      print("name = $name");
    
      if(age != null) {
        print("age = $age");
      }
    }

    // 函数调用
    showDesc("Bruce");

    // 输出结果
    name = Bruce
    age = 18
    ```
- 函数参数  
    Dart函数也可以作为参数传递  
    ```dart
    // 函数定义
    void println(String name) {
      print("name = $name");
    }

    void showDesc(var name, Function log) {
      log(name);
    }

    // 函数调用
    showDesc("Bruce", println);

    // 输出结果
    name = Bruce
    ```

### 匿名函数  

常见形式`(param){}`,使用如下:  
```dart
// 函数定义
void showDesc(var name, Function log) {
  log(name);
}

// 函数调用，匿名函数作为参数
showDesc("Bruce", (name) {
    print("name = $name");
  });

// 输出结果
name = Bruce
```

### 函数嵌套  

函数可以进行嵌套,函数定义在函数中
```dart
// 函数定义
void showDesc(var name) {
  print("That is a nested function!");
  
  //函数中定义函数
  void println(var name) {
    print("name = $name");
  }
  
  println(name);
}

// 函数调用
showDesc("Bruce");

// 输出结果
That is a nested function!
name = Bruce
```


## 类

Dart是一种面向对象的语言，具有类和基于mixin的继承。同Java一样，Dart的所有类也都继承自Object。

Dart构造函数定义为普通函数,可以定义命名构造函数:

### 构造函数

```dart
// 类定义
class Tree {
  var desc;
  
  // 命名构造函数
  Tree.init() {
    desc = "this is a seed";
  }
  
  // 函数体运行之前初始化实例变量
  Tree(var des) : desc = des;
}

// 构造函数调用
Tree t = Tree.init();
print("${t.desc}");

Tree t1 = Tree("this is a tree");
print("${t1.desc}");

// 输出结果
this is a seed
this is a tree
```


### mixin继承

mixin类似php中的代码段,提供给代码复用能力.

```dart
// 类定义
class LogUtil {
  void log() {
    print("this is a log");
  }
}

class Fruit {
  Fruit() {
    print("this is Fruit constructor with no param");
  }
}

class Apple extends Fruit with LogUtil {
  Apple():super() {
    print("this is Apple constructor with no param");
  }
}

// 调用
Apple a = Apple();
a.log(); //可执行从LogUtil继承过来的方法

// 输出结果
this is Fruit constructor with no param
this is Apple constructor with no param
this is a log
```

## 异常

Dart中的异常处理类似Java  

```dart
// 定义一个抛出异常的函数
void handleOperator() => throw Exception("this operator exception!");

// 函数调用
try {
  handleOperator();
} on Exception catch(e) {
  print(e);
} finally { // finally语句可选
  print("finally");
}

// 输出结果
Exception: this operator exception!
finally
```

## 泛型

Dart中的泛型类似Java

```dart
// 类定义
class Apple {
  var desc;
  Apple(this.desc);
  
  void log() {
    print("${this.desc}");
  }
}

class Banana {
  var desc;
  Banana(this.desc);
  
  void log() {
    print("${this.desc}");
  }
}

class FruitFactory<T> {
  T produceFruit(T t) {
    return t;
  }
}

// 调用
FruitFactory<Banana> f = FruitFactory<Banana>();
Banana b = f.produceFruit(Banana("a banana"));
b.log();
  
FruitFactory<Apple> f1 = FruitFactory<Apple>();
Apple a = f1.produceFruit(Apple("an apple"));
a.log();
  
// 输出结果
a banana
an apple  
```