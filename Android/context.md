![context1](https://github.com/musejianglan/Wiki_Note/blob/master/img/context1.png)



 大家注意看到有一些NO上添加了一些数字，其实这些从能力上来说是YES，但是为什么说是NO呢？下面一个一个解释：

​     数字1：启动Activity在这些类中是可以的，但是需要创建一个新的task。一般情况不推荐。

​     数字2：在这些类中去layout inflate是合法的，但是会使用系统默认的主题样式，如果你自定义了某些样式可能不会被使用。

​     数字3：在receiver为null时允许，在4.2或以上的版本中，用于获取黏性广播的当前值。（可以无视）

​     注：ContentProvider、BroadcastReceiver之所以在上述表格中，是因为在其内部方法中都有一个context用于使用。

​     好了，这里我们看下表格，重点看Activity和Application，可以看到，和UI相关的方法基本都不建议或者不可使用 Application，并且，前三个操作基本不可能在Application中出现。实际上，只要把握住一点，凡是跟UI相关的，都应该使用 Activity做为Context来处理；其他的一些操作，Service,Activity,Application等实例都可以，当然了，注意 Context引用的持有，防止内存泄漏。



单例模式中最好不要使用activity或者service当做context传递给单例，防止内存泄漏；

View持有Activity引用



Context的正确姿势：

1：当Application的Context能搞定的情况下，并且生命周期长的对象，优先使用Application的Context。

2：不要让生命周期长于Activity的对象持有到Activity的引用。

3：尽量不要在Activity中使用非静态内部类，因为非静态内部类会隐式持有外部类实例的引用，如果使用静态内部类，将外部实例引用作为弱引用持有。作者：尹star链接：https://www.jianshu.com/p/94e0f9ab3f1d來源：简书著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。