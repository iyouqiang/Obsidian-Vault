
精通 iOS 开发，熟练掌握Objective-C和Swift编程语言，拥有一定的逆向和安全防护经验。 （代码混淆、反调试、反注入、hook检测、越狱检测、完整性检测、加解密、重签名）
https://blog.csdn.net/u013712343/article/details/130752313

设计模式
熟悉常用的iOS应用程序架构模式，如MVC、MVVM和VIPER，能熟练运用常见的设计模式，如代理、策略等，

具有良好的编程习惯和架构能力。

熟练掌握 GCD、NSOperation、NSThread 进行多线程编程。了解 Runtime、Runloop、内存管理等底层原理。

熟练使用属性列表化、归档、NSUserDefaults、数据库、CoreData等对数据进行缓存操作。

能够熟练使用Crashlytics、Firebase、Bugly等工具进行错误监控，定位疑难杂症，确保应用稳定性。

熟悉常用的CI/CD工具，掌握fastlane和Jenkins的自动化打包和发布流程。

熟练使用Code Review工具来提高代码质量，熟悉MRC（Merge Request Code Review）和ARC代码审查流程。

熟练使用OC Lint、Clang-Format和SwiftLint等工具进行自动化Code Review，熟悉工具的部署和实现原理。

熟悉马甲包上传至App Store的全套流程，以及如何在此过程中避免常见的错误和问题。

熟悉如何对项目进行分包和组件化管理，以提高代码复用性和可维护性，减少项目开发周期和维护成本。

熟悉如何搭建一个完整的日志监控体系，包括如何收集、分析和存储日志信息，以及如何使用常用的日志监控
工具和技术来提高日志监控效率和准确性。

熟悉如何使用Shell、Python等常用脚本语言来辅助开发工作，如自动化构建、测试、部署等工作，以及如何
使用脚本来处理和分析日志信息等。

熟悉常用的算法和数据结构，如排序算法、查找算法、动态规划算法、贪心算法、字符串匹配算法等。

短剧应用开发、精准曝光、熟悉af定向推广流程、组件化分层、

攻击手段有应用脱壳、运行时分析、静态分析、动态调试、修改可执行文件、注入动态库等。
防御手段有代码混淆、反调试、反注入、Hook检测、越狱检测、完整性检测等。

技能点学习：
1、短视频
2、自动化打包
3、混淆
4、脚本学习
5、设计模式 具体设计结构
6、组件化项目
7、swift学习
8、工作表格汇总
9、支付相关项目
10、算法相关内容
11、阅读器相关项目


1、runtime

C语言中，在编译期，函数的调用就会决定调用哪个函数。而OC的函数，属于动态调用过程，在编译期并不能决定真正调用哪个函数，只有在真正运行时才会根据函数的名称找到对应的函数来调用。
Objective-C 是一个动态语言，这意味着它不仅需要一个编译器，也需要一个运行时系统来动态得创建类和对象、进行消息传递和转发。Runtime 就是这么一个主要使用 C 和汇编写的运行时库。


消息转发的过程
https://www.jianshu.com/p/d2575704e273


2、block

https://www.cnblogs.com/chglog/p/5322871.html

将函数和上下文封装起来的对象

Block的底层是一个结构体，其核心是三个部分：isa指针、描述符和捕获变量。通过LLVM编译后，你可以看到一个Block的基本结构：

struct Block_layout {
    void *isa;
    int flags;
    int reserved;
    void (*invoke)(void *, ...);
    struct {
        unsigned long int reserved;
        unsigned long int size;
        // optional helper functions
        void (*copy_helper)(void *dst, const void *src);
        void (*dispose_helper)(const void *src);
    } *descriptor;
    // captured variables
};

isa指针
指向Block在运行时的类对象。

flags
Block的消耗标志和属性位，这些标志表示Block的特性，例如是否捕获变量、Block类型等。

reserved
保留字段，通常未使用。

invoke
指向Block实现的函数指针。

descriptor
描述符，用于描述Block的附加信息，包括大小、辅助函数等。 floorTemplateJumpEvent


3、rxswift
https://juejin.cn/post/6844903912542044173

--------
iOS&js交互 https://juejin.cn/post/7197694584108089403
* 约定url协议拦截
* messageHander
* 通过代理弹窗来执行

-------
SwiftUI
* https://sspai.com/post/65567
* https://juejin.cn/post/6963881966902968357
* https://zhuanlan.zhihu.com/p/663953122
* https://www.cnblogs.com/NKnife/p/18113259 语法参考
* https://developer-rno.apple.com/cn/documentation/swiftui/

-------
rxSwift和combine


4、项目提炼，经验汇总

---------------------
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


技术栈----
1、熟悉iOS与H5交互，对js具备深入实践
2、Object-C、Swift、SwiftUI，Dark，iOS平台的flutter开发
3、shell、Python、fastlane等脚本辅助编程，开发

----------------------
面试突击课
* https://www.bilibili.com/video/BV1i94y117d3?vd_source=a40c9f5a927b93e4dc48810f20217772&spm_id_from=333.788.videopod.episodes&p=2


----------------------


Isa指针再复习：

数据结构体再复习

几种block再复习

oc和Swift再复习

自动释放池再复习



最近您可以准备下，您自己【过往项目经验和工作经历】一定要很流利得讲出来哈，大部分都是围绕之前的工作展开提问的，然后IOS相关的技术，尤其是基础原理性问题，通常大公司比较喜欢问

IOS初试：oc的week    runtime   runloop   Swift的解包原理，runtime消息调用、load和initlized区别，设计架构问题、启动优化、闪退统计问题
这些您也准备下，从其他人选那收集的，但是不全的，因为面试官很多，您都准备下，有备无患

数字马力要求挺高的，面试一定要好好准备，不打无准备的仗，如果这次面试不通过，他们后台都有记录的，下次机会就比较渺茫了，一鼓作气，先通过再说，加油哈


1、线程安全问题
2、Swift和OC的区别
3、自动释放池
4、isa指针问题
5、字符串存储问题，优化
6、滑动优化问题
7、week
8、算法问题

网络请求证书签名流程

9、你算长的，过往突出的经验，突破的技术难点

1、马甲包
2、k线绘制

--------------------------------
找出这件事情的难点+核心内容 

--------------------------------

