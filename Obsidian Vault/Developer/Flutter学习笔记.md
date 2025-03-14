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
    
### flutter