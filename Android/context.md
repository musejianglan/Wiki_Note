![context1](https://github.com/musejianglan/Wiki_Note/blob/master/img/context1.png)



 大家注意看到有一些NO上添加了一些数字，其实这些从能力上来说是YES，但是为什么说是NO呢？下面一个一个解释：

​     数字1：启动Activity在这些类中是可以的，但是需要创建一个新的task。一般情况不推荐。

​     数字2：在这些类中去layout inflate是合法的，但是会使用系统默认的主题样式，如果你自定义了某些样式可能不会被使用。

​     数字3：在receiver为null时允许，在4.2或以上的版本中，用于获取黏性广播的当前值。（可以无视）

​     注：ContentProvider、BroadcastReceiver之所以在上述表格中，是因为在其内部方法中都有一个context用于使用。

​     好了，这里我们看下表格，重点看Activity和Application，可以看到，和UI相关的方法基本都不建议或者不可使用 Application，并且，前三个操作基本不可能在Application中出现。实际上，只要把握住一点，凡是跟UI相关的，都应该使用 Activity做为Context来处理；其他的一些操作，Service,Activity,Application等实例都可以，当然了，注意 Context引用的持有，防止内存泄漏。