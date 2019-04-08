# ARTS
1.Algorithm：每周至少做一个 leetcode 的算法题

2.Review：阅读并点评至少一篇英文技术文章

3.Tip：学习至少一个技术技巧

4.Share：分享一篇有观点和思考的技术文章

## 打卡第一周

### Algorithm

#### 全集

给定一组不含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。 说明：解集不能包含重复的子集。

[subsets](https://github.com/lordlamb/leetcode/tree/master/subsets)

### Review

最近在学习Flutter，打算使用Flutter开发部分模块，所以阅读了[Add Flutter to existing apps](https://github.com/flutter/flutter/wiki/Add-Flutter-to-existing-apps)这篇文章，按照文中的方法，将Flutter以Submodule的方式集成到了目前的iOS工程里。
集成过程中遇到了一个编译问题：执行`xcode_backend.sh build`的时候，报错`FLUTTER_APPLICATION_PATH`未定义。
阅读xcode_backend.sh代码发现这个是环境变量，解决方法是在xcode_backend.sh之前定义这个变量，可以在Script中定义，也可以在.xcconfig中定义，我采用的方法是在Flutter工程目录.ios/Flutter/Generated.xcconfig中定义这个变量，注意最好使用相对路径。

### Tip
在iOS开发过程中，我们可能需要监听`UIApplicationWillTerminateNotification`通知，实现在App退出的时候保存关键数据。
但是最近在使用这个通知的时候，发现并不能正常的工作，表现为在App被Kill的时候并没有发送这个通知。查阅[Apple文档](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1623111-applicationwillterminate?language=objc)才发现这个通知不是每次都一定会通知的，原文如下：
>For apps that support background execution, this method is generally not called when the user quits the app because the app simply moves to the background in that case.

因为我们的App打开了Background Mode，所以这个通知基本上很少会触发。
那么如何来处理保存App的关键信息的场景呢？
StackOverFlow有人给出的解决方案是使用`UIApplicationDidEnterBackgroundNotification`或者使用`applicationDidEnterBackground:`，但是同时也指出这个方法无法处理SIGKILL的场景，链接在[这里](https://stackoverflow.com/questions/7818045/applicationwillterminate-when-is-it-called-and-when-not)。经过测试我也发现，如果双击Home键然后杀进程，这个通知或者说这个方法是不会执行的。
但是我也发现无论是双击Home键还是单击Home键，总是会触发这个通知`UIApplicationWillResignActiveNotification`，所以个人觉得完美的解决方案是监听通知`UIApplicationWillResignActiveNotification`。

### Share

关于[单元测试的Mock和Stub的解释](https://www.jianshu.com/p/93a21018a6ba)
