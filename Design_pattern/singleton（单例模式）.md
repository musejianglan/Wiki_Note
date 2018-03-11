### 单例(Singleton)

单例模式有以下特点：

1. 单例类只能有一个实例。
2. 单例类必须自己创建自己的唯一实例。
3. 单例类必须给所有其他对象提供这一实例。

### 恶汉模式

```
public class ASingleton{
	//私有构造
	private ASingleton(){}

	//私有静态对象
	private static ASingleton a = new ASingleton;
	//提供对外获取方法
	public static ASingleton getInstance(){
		return a;	
	}
	
}
```

### 懒汉模式

```
public class ASingleton{
	//私有构造
	private ASingleton(){}

	//私有静态对象
	private static ASingleton a;
	//提供对外获取方法
	public static ASingleton getInstance(){
		if(a == null){
			a = new ASingleton
		}
		return a;	
	}
	
}
```

### 同步锁式

```
public class ASingleton{
	//私有构造
	private ASingleton(){}

	//私有静态对象
	private static ASingleton a;
	//提供对外获取方法
	public static synchronized ASingleton getInstance(){
		if(a == null){
			a = new ASingleton
		}
		return a;	
	}
	
}
```



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

### 内部类式

```
public class ASingleton{
	//私有构造
	private ASingleton(){}

	private static class Holder{
		private static ASingleton a = new ASingleton();
	}
	//提供对外获取方法
	public static ASingleton getInstance(){
		
		return Holder.a;	
	}
	
}
```
