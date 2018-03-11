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
