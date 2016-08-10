### 模板方法(Template Method)

定义：模板方法： 定义一个操作中的算法的骨架，而将一些步骤延迟到子类中，模板方法使得子类可以不改变一个算法的结构即可重定义该算法的某些特定步骤。


### 单例(Singleton)

> 双重锁定(Double-Check Locking)

单例：保证一个类仅有一个实例，并提供一个访问它的全局访问点。

```
public class Stu {
    private static Stu ourInstance;

    public static Stu getInstance() {

        if (ourInstance == null) {
            synchronized (Stu.class) {
                if (ourInstance == null) {
                    ourInstance = new Stu();
                }
            }
        }

        return ourInstance;
    }

    private Stu() {
    }
}
```



