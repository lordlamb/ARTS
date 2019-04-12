# Algorithm

## 全排列

给定一个没有重复数字的序列，返回其所有可能的全排列。

[全排列](https://github.com/lordlamb/leetcode/tree/master/permute)

# Review

[Flutter’s Compilation Patterns](https://proandroiddev.com/flutters-compilation-patterns-24e139d14177)

这篇文章介绍了Flutter的编译模式。
目前主流的编译模式主要有JIT(Just In Time)和AOT(Ahead Of Time)两种。JIT模式的程序在运行时以程序的源代码作为输入，一边编译一边执行。AOT模式的程序在运行之前就编译为字节码或者对应体系结构的汇编或者机器指令。两者各有优劣，JIT模式的优势在于可以动态更新，劣势在于运行需要更长的时间和内存，因为运行的时候需要启动一个编译器。AOT模式的优势在于运行速度更快，适合于做复杂的运算，劣势在于不同的体系结构都需要生成一份机器指令，导致安装包体积变大，另外动态更新的效果也不好。

Flutter使用的是Dart语言，Dart语言同时支持了JIT和AOT模式，Dart语言有三种JIT模式，Script模式就是传统的JIT模式；Script Snapshot模式使用了平台无关的中间代码，优化了JIT的速度；Application Snapshot模式使用了平台相关的中间代码优化JIT的速度。Dart的AOT模式将Dart代码编译为汇编文件。

Flutter在Dart的基础上，又开发了自己的编译模式。Dart的Script和Script Snapshot模式Flutter没有使用。在iOS平台下只支持两种模式。Kernel Snapshot模式将代码先编译为平台无关的字节码，然后在Dart VM上运行，在Flutter的Debug模式下采用的是这种模式。AOT Assembly模式画与Dart的AOT模式一样，在Flutter的Release模式下使用。不同的编译模式生成不同的文件。

因为Flutter使用了两种模式，在开发过程中可以使用Kernel Snapshot模式，能够Hot Reload，减少了调试的时间。而在发布的时候可以使用AOT Assembly模式，不影响用户体验。

# Tip

WKWebView里自动播放音频：
```Objective-C
if (@available(iOS 10.0, *)) {
    config.mediaTypesRequiringUserActionForPlayback = WKAudiovisualMediaTypeNone;
} else {
    config.mediaPlaybackRequiresUserAction = NO;
}
```

# Share

[Block循环引用的分析和破解原理](https://www.jianshu.com/p/a8208307e880)
