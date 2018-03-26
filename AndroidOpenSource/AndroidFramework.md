# framework

## RX
[RxJava](https://github.com/ReactiveX/RxJava)

[RxAndroid](https://github.com/ReactiveX/RxAndroid)

### RxStore
使用RxJava协助保存和恢复对象到磁盘和从磁盘恢复对象的小型库，并观察随时间推移而发生的变化。
[RxStore](https://github.com/Gridstone/RxStore)

### reark
[reark](https://github.com/reark/reark)

## Network网络

[retrofit](https://github.com/square/retrofit)

[okhttp](https://github.com/square/okhttp)

[android-async-http](https://github.com/loopj/android-async-http)

## ImagecLoader图片加载

[ImagecLoader图片加载](https://github.com/nostra13/Android-Universal-Image-Loader)

[Android异步网络和图像加载ion](https://github.com/koush/ion)

[glide](https://github.com/bumptech/glide)

[facebook/fresco](https://github.com/facebook/fresco)

[picasso](https://github.com/square/picasso)

## 图片压缩

### Tiny
这是本列表中的第二个框架。它负责图像压缩，功能相当强大的。还支持

使用异步线程池来压缩图像，并且当压缩完成时，会将结果发送到主线程中。  
[github](Tiny)

## Dependency Injection依赖注入

[dagger](https://github.com/square/dagger)

[butterknife](https://github.com/JakeWharton/butterknife)



Dagger	

Android Annotations	

Roboguice

## json

[fastjson](https://github.com/alibaba/fastjson)

[gson](https://github.com/google/gson)

## DataBase


### realm
Realm是一款直接在手机，平板电脑或可穿戴设备中运行的移动数据库。该存储库包含Realm的Java版本的源代码，该版本目前仅在Android上运行。
[realm](https://github.com/realm/realm-java)

### for database
Reactive API for SQLiteDatabase and ContentResolver.  
[github](https://github.com/pushtorefresh/storio)

## Event

[EventBus](https://github.com/greenrobot/EventBus)


Otto

![img]()  
[github]()

## HotFix热修复

## 下载

### PRDownloader
这是一个为 Android 提供的支持断点续传的文件下载器。  

> PRDownloader 可以用来下载 image、video、pdf、apk 等等任意类型的文件。
> 支持断点续传。
> 支持大文件下载。
> 有简单的接口做下载请求。
> 我们可以用给的下载Id检查下载的状态。
> PRDownloader 在下载文件时，提供了像 onProgress、onCancel、onStart、onError 等等的回调。
> 支持适当的请求取消。
> 多个请求可以并行实现。
> 所有类型的自定义都是可能的。

![1](https://static.oschina.net/uploads/space/2018/0117/162617_zvUX_2896879.png)  
[github](https://github.com/MindorksOpenSource/PRDownloader)

## fragment

### FragmentRigger
该库使用一种强大的方法来管理 Fragment。其目标是使得 Fragment 易于使用，并将管理它们的成本最小化。
![图片](https://github.com/JustKiddingBaby/FragmentRigger/blob/master/images/show.gif?raw=true)  
[FragmentRigger](https://github.com/JustKiddingBaby/FragmentRigger)

## log

### hyperlog-android

这是一个公用工具日志库，位于标准的 Android 日志类之上，用于存储数据库中的日志，并将它们推入远程服务器进行调试。


![img](https://static.oschina.net/uploads/space/2018/0117/163309_jvSM_2896879.gif)  
[github](https://github.com/hypertrack/hyperlog-android)


## theme主题

### Aesthetic
这是一个新的库，仍处于测试版，但它做了一件非常酷的事情 - 它通过 Rx 支持动态改变系统主题！ 作者是这么描述的：

一个快速和易于使用的即插即用的动态主题引擎。由 Rx 支持，适用于 Android 应用。  
![img](https://static.oschina.net/uploads/space/2017/0523/113907_V3h0_2896879.png)  
[github](https://github.com/afollestad/aesthetic)

## degub

[Android和Java的内存泄漏检测库](https://github.com/square/leakcanary)

### stetho
Stetho是Android应用程序的一个复杂的调试桥梁。启用后，开发人员可以使用Chrome桌面浏览器本身的Chrome开发者工具功能。开发人员还可以选择启用可选dumpapp工具，该 工具为应用程序内部提供强大的命令行界面。  
[stetho](https://github.com/facebook/stetho)

### Fairy
airy 是一个简单的调试工具，允许开发者使用 adb logcat 命令在 Android 手机上查看 Android 系统日志，而不是在电脑上。

它还允许在任何地方使用 Android 手机扫描系统日志信息，甚至不需要 root。

![img](https://static.oschina.net/uploads/space/2018/0117/163347_5x9V_2896879.png)  
[github](https://github.com/Zane96/Fairy)

### AppMethodOrder
一个能让你了解所有函数调用顺序以及函数耗时的 Android 库（无需侵入式代码）。

> 当项目代码量很大的时候，或者你作为一名新人要快速掌握代码的时候，给函数打上 log ，来了解代码执行逻辑，这种方式会显然成本太大，要改动项目编译运行，NO！太耗时；或者你想 debug 的方式来给你想关注的几个函数，来了解代码执行逻辑，NO！因为你肯定会漏掉函数；也许你可以固执的给你写的项目打满 log 说这样也行，但是你要知道你方法所调用的 jdk 的函数或者第三方 aar 或者 jar 再或者 android sdk 中的函数调用顺序你怎么办，还能打 log 吗？显然不行吧，来~这个项目给让可以让你以包名为过滤点过滤你想要知道所有函数调用顺序。  

![1](https://static.oschina.net/uploads/space/2017/0523/113727_oLqv_2896879.png)  
[github](https://github.com/zjw-swun/AppMethodOrder)

### Android DebugKit
这是一个有趣的库。它允许你创建和使用特殊的悬停调试工具，以触发你在应用程序中定义的操作。这些操作可以在运行时明显的触发，因此可以在编写或测试手机屏幕反馈时间时使用。

该库使用 Builder 模式。 它很容易使用，在 README 中有一个其用法的示例。  
![img](https://static.oschina.net/uploads/space/2017/0523/113842_Tfth_2896879.gif)  
[github](https://github.com/hulab/debugkit)

### BlockCanaryEx
这是一个当你的应用程序被阻塞时，它可以方便在代码中找到阻塞的方法的库。

![img](https://static.oschina.net/uploads/space/2017/0523/114421_vPtM_2896879.png)  
[github](https://github.com/seiginonakama/BlockCanaryEx)

![img]()  
[github]()

## 加密

### Cipher.so

该库提供了一种将敏感数据加密到原生 .so 库的简单方法。

[github](该库提供了一种将敏感数据加密到原生 .so 库的简单方法。)

## Kotlin

### kotlin-math

使得图形数学算法写起来更轻松的 Kotlin API 的集合。这些 API 大多都是在 GLSL (OpenGL Shading Language) 之后建模的，以便使从着色器或者向着色器移植代码更轻松。
 
[github](https://github.com/romainguy/kotlin-math)

## 架构

### android-clean-architecture-mvi-boilerplate

这是使用 Model-View-Intent 模式的一个 Buffer 的分支，是干净的应用架构样板。

在展现层它现在使用的是来自 Android Architecture Components Library 的 ViewModel。缓存层现在也使用了 Room。

[github](https://github.com/bufferapp/android-clean-architecture-mvi-boilerplate)

### Litho
itho 不是库，而是一个框架。它是一个非常强大的框架，以声明的方式构建 UI。它由 Facebook 的开发者开发，所以就算你不想使用它，它仍然值得你去关注它的开发过程。  
主要特性包括：

> 使用申明式 API  来定义 UI 组件。你只需要基于一套固定的输入来描述布局就好，其它事情框架会搞定。  
> 异步布局：Litho 可以在不阻碍 UI 线程的情况下计算并对 UI 布局。  
> 扁平化视图：Litho 使用 Yoga 来布局，并自动缩减 UI中 ViewGroups 的数量。  
> 细粒度回收：UI 中任何像 text 或 image 之类的组件都能被回收再利用。  
[github](https://github.com/facebook/litho)


![img]()  
[github]()

# 功能

[二维码](https://github.com/zxing/zxing)



