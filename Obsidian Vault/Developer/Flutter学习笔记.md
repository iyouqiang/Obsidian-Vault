[Flutter实战](https://book.flutterchina.club/chapter1/flutter_intro.html#_1-2-3-%E5%A6%82%E4%BD%95%E5%AD%A6%E4%B9%A0flutter)
### 一、资源

- **官网**：阅读Flutter官网的资源是快速入门的最佳方式，同时官网也是了解最新Flutter发展动态的地方，由于目前 Flutter 仍然处于快速发展阶段，所以建议读者还是时不时的去官网看看有没有新的动态。
    
- **源码及注释**：**源码注释应作为学习 Flutter 的第一文档**，Flutter SDK 的源码是包含在 Flutter 工程中的，并且注释非常详细且有很多示例，我们可以通过 IDE 的跳转功能快速定位到源码。实际上，Flutter 官方的组件文档就是通过注释生成的。根据笔者经验，源码结合注释可以帮我们解决大多数问题。
    
- **Github**：如果遇到的问题在StackOverflow上也没有找到答案，可以去 Github flutter 项目下提 issue。
    
- **Gallery源码**：Gallery 是 Flutter 官方示例 APP，里面有丰富的示例，读者可以在网上下载安装。Gallery 的源码在 Flutter 源码 “examples” 目录下。
    
- **StackOverflow**： StackOverflow 是目前全球最大的程序员问答社区，现在也是活跃度最高的 Flutter 问答社区。StackOverflow 上面除了世界各地的 Flutter开发者会在上面交流之外，Flutter 开发团队的成员也经常会在上面回答问题。
    
 [Flutter教程#](https://book.flutterchina.club/chapter1/flutter_intro.html#_2-%E5%B0%8F%E7%BB%93)    [Dark语法](https://dart.cn/language/)

### 二、开发环境搭建

推荐工具：
IDE推荐：
- visual  Studio Code  内置AI，编码高效
插件安装：搜索快捷键：shift + command + p
推荐主题：
- Atom Material Theme
推荐插件：
* Dart Data Class Generator
* ErrorLens
* Pubspec Assist
* GitHub Copilot

### 三、开发纪要

### Dart

 1. **官方文档**
- **Dart 语言官方文档**: [Dart Language Tour](https://dart.dev/guides/language/language-tour)
    
    - 这是 Dart 官方提供的语言指南，涵盖了 Dart 的核心语法和特性，适合初学者和有经验的开发者。
        
 
 2. **视频教程**

- **Dart Programming Tutorial - Full Course**: [YouTube](https://www.youtube.com/watch?v=Ej_Pcr4uC2Q)
    
    - 这是一个免费的 Dart 编程完整课程，适合初学者。
        
- **Flutter & Dart - The Complete Flutter App Development Course**: [YouTube](https://www.youtube.com/watch?v=x0uinJvhNxI)
    
    - 虽然主要针对 Flutter，但也详细讲解了 Dart 语法。
        

 3. **互动学习平台**

- **DartPad**: [DartPad](https://dartpad.dev/)
    
    - 一个在线 Dart 代码编辑器，适合边学边练。
        
- **Exercism Dart Track**: [Exercism](https://exercism.io/tracks/dart)
    
    - 提供 Dart 编程练习，适合通过实践学习。
        

 4. **社区和论坛**

- **Dart 官方社区**: [Dart Community](https://dart.dev/community)
    
    - 可以在这里提问、分享经验，获取帮助。
        
- **Stack Overflow**: [Dart Questions](https://stackoverflow.com/questions/tagged/dart)


### 创建 Dart 项目

1. **创建一个新的 Dart 项目**  
    打开 VS Code，按下 `Ctrl+Shift+P`（或 `Cmd+Shift+P` 在 macOS 上），在命令面板中输入并==选择 `Dart: New Project`。然后选择 "Console Application"（命令行应用）== ，为你的项目选择一个合适的文件夹和名称。 终端 `dart run`
    

### **1. `mixin` 的用法**

`mixin` 是 Dart 中专门用于代码复用的关键字，**只能通过混入（`with`）的方式被其他类或 `mixin` 使用**，**不能直接实例化**。

#### **定义方式**：

```
mixin MyMixin {
  void log(String message) {
    print('Mixin Log: $message');
  }
}
```

#### **使用限制**：

- **不能有构造函数**（无法通过 `MyMixin()` 创建实例）。
    
- **可以包含方法实现和属性**。
    
- **可以指定依赖类型**（通过 `on` 关键字限定混入的基类）。
    

#### **示例**：

```
class Animal {
  void eat() => print('Eating...');
}

// ==MyMixin 只能被混入到 Animal 或其子类==
mixin MyMixin on Animal {
  void logAction() => print('Action logged!');
}

class Dog extends Animal with MyMixin {
  void bark() => print('Woof!');
}

void main() {
  var dog = Dog();
  dog.eat();      // 继承自 Animal
  dog.logAction(); // 来自 MyMixin
  dog.bark();     // Dog 自身的方法
}
```
---

### **2. `mixin class` 的用法**

`mixin class` 是 Dart 3.0 引入的新语法，**允许一个类同时作为普通类和 `mixin` 使用**。这种类既可以被继承（`extends`），也可以被混入（`with`）。

#### **定义方式**：

```
mixin class MyMixinClass {
  void printMessage(String msg) {
    print('Message: $msg');
  }
}
```
#### **使用限制**：

- **可以有构造函数**（但作为 `mixin` 混入时，构造函数会被忽略）。
    
- **既可以作为普通类继承，也可以作为 `mixin` 混入**。
    
#### **示例**：

```
// 作为普通类继承
class BaseClass extends MyMixinClass {
  void baseMethod() => print('Base method');
}

// 作为 mixin 混入
class CombinedClass with MyMixinClass {
  void combinedMethod() => print('Combined method');
}

void main() {
  var base = BaseClass();
  base.printMessage('Hello'); // 来自 MyMixinClass
  base.baseMethod();

  var combined = CombinedClass();
  combined.printMessage('Hi'); // 来自 MyMixinClass
  combined.combinedMethod();
}
```
---

### **3. 核心区别对比**

|**特性**|**`mixin`**|**`mixin class`**|
|---|---|---|
|**定义关键字**|`mixin`|`mixin class`|
|**能否直接实例化**|❌ 不能|✅ 可以|
|**能否被继承（`extends`）**|❌ 不能|✅ 可以|
|**能否被混入（`with`）**|✅ 只能被混入|✅ 可以作为混入|
|**构造函数**|❌ 禁止|✅ 可以有构造函数|
|**依赖限制（`on`）**|✅ 支持|❌ 不支持|

---

### **4. 如何选择？**

- **使用 `mixin`**：  
    当需要**纯粹复用代码逻辑**且无需实例化时（例如日志工具、验证逻辑）。
    
- **使用 `mixin class`**：  
    当需要**一个既能复用代码又能独立实例化**的类时（例如基础工具类，既可以直接使用，也可混入其他类）。
    

---

### **5. 代码示例对比**

#### **`mixin` 的典型场景**：
```
mixin Logger {
  void log(String msg) => print('Log: $msg');
}

class User with Logger {
  void login() {
    log('User logged in');
  }
}
```
#### **`mixin class` 的典型场景**：

```
mixin class CacheManager {
  final Map<String, dynamic> _cache = {};

  void cacheData(String key, dynamic value) {
    _cache[key] = value;
  }

  dynamic getData(String key) => _cache[key];
}

// 直接实例化
var cache = CacheManager();
cache.cacheData('token', 'abc123');

// 混入到其他类
class AppService with CacheManager {
  void initialize() {
    cacheData('config', {});
  }
}
```

---

### **总结**

- `mixin` 是**纯复用逻辑**的工具，强调无状态和非实例化。
    
- `mixin class` 是**混合类**，既能复用逻辑又能独立存在。
    
- 根据是否需要实例化或继承来选择使用哪种方式。