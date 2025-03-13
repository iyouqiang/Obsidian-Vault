
### 文档指引

* https://sspai.com/post/65567
* https://juejin.cn/post/6963881966902968357
* https://zhuanlan.zhihu.com/p/663953122
* https://www.cnblogs.com/NKnife/p/18113259 
* https://developer-rno.apple.com/cn/documentation/swiftui/
* https://developer.apple.com/tutorials/SwiftUI  教程

https://www.bilibili.com/video/BV14z4y1d7b4?t=5
斯坦福公开课 CS193P·2020 年春：该课程强推，我当年学习 OC 看的就是它，现在到SwiftUI了还是先看这个，系统且细致，结合案例和编程过程中的小技巧介绍，是很好的入门课程。

https://developer.apple.com/tutorials/swiftUI/
苹果官方 SwiftUI 课程：打开Xcode，照着官方的教学，从头到尾学着做一遍应用。

https://sspai.com/link?target=https%3A%2F%2Fwww.hackingwithswift.com%2F100%2FswiftUI
Hacking with swift：这是国外一个程序员用业余时间搭建的分享网站，有大量的文章可以阅读，还有推荐初学者跟着做的「100 Days of SwiftUI」课程。

https://developer.apple.com/documentation/
苹果官方文档：文档是必读的，虽然很多文档缺乏工程细节，但是文档涉及很多概念性的内容，你可以知道官方是怎么思考的，并且有很多具体的机制参数。我本人有一个习惯，要是工程涉及某个框架，会把相关的文档都翻译一遍。

https://sspai.com/link?target=https%3A%2F%2Fstackoverflow.com%2F
Stack Overflow：有问题查询专用，在谷歌中搜索错误代码或者关键词基本都会由该网站给答案。
阅读 SwiftUI 库的源代码。


### 知识点纪要

在最新版本的 **SwiftUI** 中，使用状态关键字来管理视图的状态是非常重要的，尤其是在响应式编程中。随着 **SwiftUI** 和 **Swift** 语言的进化，状态管理方式有所变化。以下是一些常用的状态关键字及其使用时机：

### 1. `@State`

`@State` 用于表示视图的局部状态，它会创建一个值并使得视图能够根据该值的变化重新渲染。

- **使用时机**：当需要管理与视图相关的简单状态时，使用 `@State`。它通常用于绑定到界面元素，如按钮的状态、文本框的输入等。
    
- **示例**：
```
    struct ContentView: View {
    @State private var count = 0

    var body: some View {
        VStack {
            Text("Count: \(count)")
            Button("Increment") {
                count += 1
            }
        }
    }
}

```

### 2. `@Binding`

`@Binding` 是一种双向绑定，允许子视图读取和修改父视图中的状态值。

- **使用时机**：当子视图需要修改父视图的 `@State` 或其他可变数据时，使用 `@Binding`。这是用来将父视图的状态传递给子视图。
    
- **示例**：
```
struct ParentView: View {
    @State private var count = 0

    var body: some View {
        ChildView(count: $count)
    }
}

struct ChildView: View {
    @Binding var count: Int

    var body: some View {
        Button("Increment") {
            count += 1
        }
    }
}

```

### 3. `@ObservedObject`

`@ObservedObject` 用于观察一个 **外部对象** 的状态，并在对象的值发生变化时重新渲染视图。被观察的对象通常是遵循 `ObservableObject` 协议的类。

- **使用时机**：当你需要从视图外部管理状态时（如网络请求或模型数据），使用 `@ObservedObject`。它适用于多个视图共享同一个数据模型。
    
- **示例**：
```
class Counter: ObservableObject {
    @Published var count = 0
}

struct ContentView: View {
    @ObservedObject var counter = Counter()

    var body: some View {
        VStack {
            Text("Count: \(counter.count)")
            Button("Increment") {
                counter.count += 1
            }
        }
    }
}

```

>`@Published` 是 Swift 中的一种属性包装器（Property Wrapper），它是 **SwiftUI** 和 **Combine 框架** 中的关键特性之一，用来标记那些需要**发布变化的属性**。当你希望某个属性的值变化时，能够通知绑定到该属性的观察者进行更新，通常会使用 `@Published`。

### 基本概念：

`@Published` 用于 **ObservableObject** 类中的属性，它会自动生成一个 **Publisher**，用于广播属性值的变化。当属性值发生变化时，任何观察该属性的视图或对象都会收到通知，从而触发相应的更新。

### 适用场景：

当你在自定义的模型或视图模型中定义一个可观察的属性，并希望在属性值变化时通知界面进行更新时，使用 `@Published`。这种特性通常配合 `@ObservedObject` 或 `@StateObject` 一起使用。

### 4. `@EnvironmentObject`

`@EnvironmentObject` 是一个全局状态管理工具，它允许你在视图树的任何地方共享数据，而不需要手动传递绑定。

- **使用时机**：当多个视图层级需要共享同一数据时，使用 `@EnvironmentObject`。例如，应用程序设置、用户认证信息等跨视图的状态。
    
- **示例**：
```
class UserSettings: ObservableObject {
    @Published var isDarkMode = false
}

struct ContentView: View {
    @EnvironmentObject var settings: UserSettings

    var body: some View {
        Toggle(isOn: $settings.isDarkMode) {
            Text("Dark Mode")
        }
    }
}

struct AppView: View {
    var body: some View {
        ContentView()
            .environmentObject(UserSettings())
    }
}

```

### 5. `@StateObject`

`@StateObject` 是用于创建和管理 `ObservableObject` 的状态。它与 `@ObservedObject` 类似，但在创建视图时初始化并管理对象的生命周期。

- **使用时机**：当你在视图内创建并管理一个 `ObservableObject` 时，使用 `@StateObject`。确保该对象只会在视图的生命周期内初始化一次。
    
- **示例**：
```
class Counter: ObservableObject {
    @Published var count = 0
}

struct ContentView: View {
    @StateObject private var counter = Counter()

    var body: some View {
        VStack {
            Text("Count: \(counter.count)")
            Button("Increment") {
                counter.count += 1
            }
        }
    }
}

```

### 6. `@Environment`

`@Environment` 用于获取从环境中传递的值。它通常用于获取系统提供的环境值（如颜色、字体等）或应用==自定义的全局环境数据==。

- **使用时机**：当你需要访问系统的环境变量（如颜色、字体等），或访问应用程序的环境设置时，使用 `@Environment`。
    
- **示例**：
```
  struct ContentView: View {
    @Environment(\.colorScheme) var colorScheme

    var body: some View {
        Text("Hello, World!")
            .foregroundColor(colorScheme == .dark ? .white : .black)
    }
}

```

### 小结

1. **@State**：视图的局部状态。
2. **@Binding**：在父视图和子视图之间传递可变的状态。
3. **@ObservedObject**：观察外部的对象，通常用于模型数据的变化。
4. **@EnvironmentObject**：全局共享的对象，适合跨视图树共享。
5. **@StateObject**：创建和管理一个 `ObservableObject` 的状态，确保它在视图内初始化一次。
6. **@Environment**：访问系统或应用提供的环境数据。

**使用时机**：你选择哪种状态管理方式取决于数据的使用范围、生命周期以及你希望如何在视图之间共享数据。

### 7. `@Bindable`

在 SwiftUI 中，`@Bindable` 是一个用于标记对象的属性包装器（Property Wrapper）。它主要用于 **绑定对象**，并使其支持 **双向绑定**（two-way binding），从而使视图能够与该对象的状态进行交互。

### 作用：

`@Bindable` 修饰的属性通常用于 **可观察的对象**，使得这个对象能够自动更新视图中的绑定值，并且当视图中的数据变化时，能自动反向更新模型对象中的数据。

### 何时使用 `@Bindable`：

- 当你有一个可观察对象（`ObservableObject`）并希望能够在视图中直接修改它时，使用 `@Bindable` 使它能够参与视图的绑定。
- 它用于支持双向绑定，通常与 `@State`, `@Binding`, 或 `@ObservedObject` 配合使用。

### 基本用法：

```
class ModelData: ObservableObject {
    @Published var name = "John"
}

```

然后在视图中使用：
```
@Bindable var modelData = ModelData()
```
这里的 `modelData` 将会自动与视图绑定，在视图中修改它时，模型中的数据会被同步更新。

### 与 `@Binding` 和 `@State` 的关系：

- `@Binding` 用于 **父视图与子视图之间的双向数据绑定**。父视图可以通过 `@Binding` 将数据传递给子视图，并允许子视图修改这些数据。
- `@State` 是一个视图局部的 **状态属性**，它用于保存和管理视图的局部状态。它是一个 **值类型**。
- `@Bindable` 用于标记一个对象，使它能够绑定并支持 **双向绑定**，它通常用于一个 **引用类型**（`ObservableObject`）的状态，像 `ModelData` 这样的可观察对象。

### 示例：

假设你有一个 `ModelData` 类，它包含一些数据，并希望这个数据能够与视图绑定：
```
class ModelData: ObservableObject {
    @Published var name = "John"
}

```

然后在你的视图中，使用 `@Bindable` 来实现绑定：
```
struct ContentView: View {
    @Bindable var modelData = ModelData()

    var body: some View {
        VStack {
            TextField("Name", text: $modelData.name) // 双向绑定
            Text("Hello, \(modelData.name)") // 自动更新视图
        }
    }
}

```
在这个例子中，`modelData.name` 的值被绑定到 `TextField`，并且视图会随着 `name` 的变化自动更新。当你修改 `TextField` 的内容时，`modelData.name` 的值也会改变，反之亦然。

### 总结：

`@Bindable` 修饰符使得可观察的对象（`ObservableObject`）能够参与视图的双向数据绑定，并能使视图与对象的状态进行交互。这是实现 **双向绑定** 的关键，通常与其他属性包装器（如 `@State`、`@Binding` 和 `@ObservedObject`）一起使用。

### 8. `@`Published``

在 SwiftUI 中， 是一个用于属性的 **属性包装器**，它的作用是让一个类的属性变得 **可观察**，并且当这个属性发生变化时，会通知所有订阅该属性的视图进行更新。

### 主要作用：

- **自动通知变化**：`@Published` 会将属性变为 **可观察的**（`ObservableObject`）。当属性的值发生变化时，所有绑定到这个属性的视图会自动更新。
- **与 `ObservableObject` 配合使用**：`@Published` 通常用在 **`ObservableObject`** 中，表示属性会在变化时触发视图更新。

### 使用场景：

- 当你需要监控一个属性的变化，并希望视图在这个属性变化时自动更新，使用 `@Published` 来标记这个属性。
- 它主要用于 **数据模型** 中的属性，通过与 `@State`、`@Binding` 和 `@ObservedObject` 等视图属性配合使用，完成数据的双向绑定。

### 详细说明：

1. **声明类时的使用**： `@Published` 用于声明类中的一个属性，这样当该属性的值变化时，会自动通知所有观察它的视图进行更新。
    
```
    class UserData: ObservableObject {
    @Published var name: String
    
    init(name: String) {
        self.name = name
    }
}
```
    
2. **视图中的使用**： 在 SwiftUI 视图中，可以通过 `@ObservedObject` 或 `@StateObject` 来订阅 `@Published` 属性的变化。
```
    struct ContentView: View {
    @ObservedObject var userData = UserData(name: "John")
    
    var body: some View {
        VStack {
            Text(userData.name)  // 自动更新
            Button("Change Name") {
                userData.name = "Jane"  // 改变属性值，视图自动更新
            }
        }
    }
}
```
    在上面的代码中，当 `userData.name` 的值发生变化时，`Text` 视图会自动更新，显示新的名字。
    

### 核心概念：

- `@Published` 主要作用是 **通知观察者属性发生了变化**，并自动触发视图更新。在 `ObservableObject` 中标记某个属性为 `@Published`，意味着当这个属性的值改变时，所有绑定这个对象的视图都会被刷新。
- 它不需要手动调用更新函数，`SwiftUI` 会自动处理更新过程。

### 示例：
```
class UserData: ObservableObject {
    @Published var name: String
    @Published var age: Int
    
    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
}
```
然后在视图中使用 `@ObservedObject` 来观察这些属性的变化：

```
struct ContentView: View {
    @ObservedObject var userData = UserData(name: "Alice", age: 30)
    
    var body: some View {
        VStack {
            Text("Name: \(userData.name)")
            Text("Age: \(userData.age)")
            
            Button("Change Name") {
                userData.name = "Bob"  // 修改属性值，视图自动更新
            }
        }
    }
}
```

每当你点击按钮改变 `name` 或 `age` 时，视图会自动更新。

### 总结：

`@Published` 是一种非常方便的方式来 **自动观察** 数据的变化，并让视图实时响应这些变化。它使得数据模型与视图之间的绑定更加高效和简洁，尤其在涉及到 **动态变化的视图** 时，使用 `@Published` 可以帮助简化代码和保持状态同步。

# Swift 第一轮学习总结
#### SwiftUI与现有项目交互

**SwiftUI对接现有项目**
Coordinator
UIViewRepresentable/UIViewControllerRepresentable

**现有项目对接SwiftUI**
UIHostingController

记忆提取key:  Swift UI

| 优势                        | SwiftUI 提供的能力                                    |
| ------------------------- | ------------------------------------------------ |
| **声明式 UI** /S             | 代码更简洁，逻辑更清晰                                      |
| **少代码，高效开发** /t           | 避免手写 `Storyboard` 和 `Auto Layout`                |
| **响应式数据绑定** /f            | `@State` `@Binding` `@ObservedObject` 让 UI 与数据同步 |
| **跨平台支持** /               | iOS、macOS、watchOS、tvOS 共享 UI 代码                  |
| **实时预览（Live Preview）** /i | Xcode 直接预览 UI，无需运行 App                           |
| **内置动画支持** /I             | `withAnimation` 实现丝滑动画                           |
| **兼容 UIKit**  /U          | 可混合使用 `UIViewControllerRepresentable`            |
| **适用于 MVVM 架构** /W        | 结合 `Combine` 更现代化                                |

