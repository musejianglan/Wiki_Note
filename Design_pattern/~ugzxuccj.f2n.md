# 设计模式中类的关系
在java以及其他的面向对象设计模式中，类与类之间主要有6种关系，他们分别是：依赖、关联、聚合、组合、继承、实现。他们的耦合度依次增强。

### 依赖（Dependence）
![图片描述](https://raw.githubusercontent.com/musejianglan/Wiki_Note/master/Design_pattern/img/Dependence.png)

> 定义：对于两个相对独立的对象，当一个对象负责构造另一个对象的实例，或者依赖另一个对象的服务时，这两个对象之间主要体现为依赖关系。

> 类A当中使用了类B，其中类B是作为类A的方法参数、方法中的局部变量、或者静态方法调用。类上面的图例中：People类依赖于Book类和Food类，Book类和Food类是作为类中方法的参数形式出现在People类中的。

```
public class People{  
    //Book作为read方法的形参  
     public void read(Book book){  
        System.out.println(“读的书是”+book.getName());  
    }  
}  
```

### 关联（Association）
单向关联：  
![图片描述](https://raw.githubusercontent.com/musejianglan/Wiki_Note/master/Design_pattern/img/Association1.png)

双向关联  
![图片描述](https://raw.githubusercontent.com/musejianglan/Wiki_Note/master/Design_pattern/img/Association2.png)

> 定义:对于两个相对独立的对象，当一个对象的实例与另一个对象的一些特定实例存在固定的对应关系时，这两个对象之间为关联关系。关联关系分为单向关联和双向关联。

> 在java中，单向关联表现为：类A当中使用了类B，其中类B是作为类A的成员变量。双向关联表现为：类A当中使用了类B作为成员变量；同时类B中也使用了类A作为成员变量。


```
public class Son{  

   //关联关系中作为成员变量的类一般会在类中赋值  
    Father father = new Father();  
    public void getGift(){  
        System.out.println(“从”+father.getName()+”获得礼物”);  
    }  
}  
  
public class Father{  
    Son son = new Son();  
    public void giveGift(){  
        System.out.println(“送给”+son.getName()+“礼物”);  
    }  
}  
```

### 聚合（Aggregation）
![图片描述](https://raw.githubusercontent.com/musejianglan/Wiki_Note/master/Design_pattern/img/Aggregation.png)

> 定义： 聚合关系是关联关系的一种，耦合度强于关联，他们的代码表现是相同的，仅仅是在语义上有所区别：关联关系的对象间是相互独立的，而聚合关系的对象之间存在着包容关系，他们之间是“整体-个体”的相互关系。

```
public class People{  
    Car car;  
    House house;   
    //聚合关系中作为成员变量的类一般使用set方法赋值  
     public void setCar(Car car){  
        This.car = car;  
    }  
    public void setHouse(House house){  
        This.house = house;  
    }  
  
    public void driver(){  
        System.out.println(“车的型号：”+car.getType());  
    }  
    public void sleep(){  
        System.out.println(“我在房子里睡觉：”+house.getAddress());  
    }  
}  
```

### 组合（Composition）
![图片描述](https://raw.githubusercontent.com/musejianglan/Wiki_Note/master/Design_pattern/img/Composition.png)
> 定义： 相比于聚合，组合是一种耦合度更强的关联关系。存在组合关系的类表示“整体-部分”的关联关系，“整体”负责“部分”的生命周期，他们之间是共生共死的；并且“部分”单独存在时没有任何意义。

> People与Soul、Body之间是组合关系，当人的生命周期开始时，必须同时有灵魂和肉体；当人的生命周期结束时，灵魂肉体随之消亡；无论是灵魂还是肉体，都不能单独存在，他们必须作为人的组成部分存在。

```
Public class People{  
    Soul soul;  
    Body body;   
    //组合关系中的成员变量一般会在构造方法中赋值  
     Public People(Soul soul, Body body){   
        This.soul = soul;  
        This.body = body;  
    }  
  
    Public void study(){  
        System.out.println(“学习要用灵魂”+soul.getName());  
    }  
    Public void eat(){  
        System.out.println(“吃饭用身体：”+body.getName());  
    }  
}  
```

### 继承（Generalization）
![图片描述](https://raw.githubusercontent.com/musejianglan/Wiki_Note/master/Design_pattern/img/Generalization.png)

> 定义： 继承表示类与类（或者接口与接口）之间的父子关系。

> 在java中，用关键字extends表示继承关系。UML图例中，继承关系用实线+空心箭头表示，箭头指向父类。



### 实现（Implementation）
![图片描述](https://raw.githubusercontent.com/musejianglan/Wiki_Note/master/Design_pattern/img/Implementation.png)

> 定义： 表示一个类实现一个或多个接口的方法。接口定义好操作的集合，由实现类去完成接口的具体操作。

> 在java中使用implements表示。UML图例中，实现关系用虚线+空心箭头表示，箭头指向接口。



|模式|描述|包括|
|--|--|--|
|创建型模式|这些设计模式提供了一种在创建对象的同时隐藏创建逻辑的方式，而不是使用 new 运算符直接实例化对象。这使得程序在判断针对某个给定实例需要创建哪些对象时更加灵活。|工厂模式（Factory Pattern）抽象工厂模式（Abstract Factory Pattern）单例模式（Singleton Pattern）建造者模式（Builder Pattern）原型模式（Prototype Pattern）|
|结构型模式|这些设计模式关注类和对象的组合。继承的概念被用来组合接口和定义组合对象获得新功能的方式。|适配器模式（Adapter Pattern）桥接模式（Bridge Pattern）过滤器模式（Filter、Criteria Pattern）组合模式（Composite Pattern）装饰器模式（Decorator Pattern）外观模式（Facade Pattern）享元模式（Flyweight Pattern）代理模式（Proxy Pattern）|
|行为型模式|这些设计模式特别关注对象之间的通信。|责任链模式（Chain of Responsibility Pattern）命令模式（Command Pattern）解释器模式（Interpreter Pattern）迭代器模式（Iterator Pattern）中介者模式（Mediator Pattern）备忘录模式（Memento Pattern）观察者模式（Observer Pattern）状态模式（State Pattern）空对象模式（Null Object Pattern）策略模式（Strategy Pattern）模板模式（Template Pattern）访问者模式（Visitor Pattern）|
|J2EE 模式|这些设计模式特别关注表示层。这些模式是由 Sun Java Center 鉴定的。|MVC 模式（MVC Pattern）业务代表模式（Business Delegate Pattern）组合实体模式（Composite Entity Pattern）数据访问对象模式（Data Access Object Pattern）前端控制器模式（Front Controller Pattern）拦截过滤器模式（Intercepting Filter Pattern）服务定位器模式（Service Locator Pattern）传输对象模式（Transfer Object Pattern）|


* 创建型模式-->对象怎么来
* 结构型模式-->对象和谁有关
* 行为型模式-->对象与对象在干嘛
* J2EE 模式-->对象合起来要干嘛（表现层,文中表示层个人感觉用的不准确）java是面向对象的语言,所以要搞好对象,模式（套路）就是用来更加好的搞对象滴。


![设计模式](https://raw.githubusercontent.com/musejianglan/Wiki_Note/master/Design_pattern/img/the-relationship-between-design-patterns.jpg)

### 设计模式的6大原则
##### 1、开闭原则（Open Close Principle）

开闭原则的意思是：对扩展开放，对修改关闭。在程序需要进行拓展的时候，不能去修改原有的代码，实现一个热插拔的效果。简言之，是为了使程序的扩展性好，易于维护和升级。想要达到这样的效果，我们需要使用接口和抽象类，后面的具体设计中我们会提到这点。

##### 2、里氏代换原则（Liskov Substitution Principle）

里氏代换原则是面向对象设计的基本原则之一。 里氏代换原则中说，任何基类可以出现的地方，子类一定可以出现。LSP 是继承复用的基石，只有当派生类可以替换掉基类，且软件单位的功能不受到影响时，基类才能真正被复用，而派生类也能够在基类的基础上增加新的行为。里氏代换原则是对开闭原则的补充。实现开闭原则的关键步骤就是抽象化，而基类与子类的继承关系就是抽象化的具体实现，所以里氏代换原则是对实现抽象化的具体步骤的规范。

##### 3、依赖倒转原则（Dependence Inversion Principle）

这个原则是开闭原则的基础，具体内容：针对接口编程，依赖于抽象而不依赖于具体。

##### 4、接口隔离原则（Interface Segregation Principle）

这个原则的意思是：使用多个隔离的接口，比使用单个接口要好。它还有另外一个意思是：降低类之间的耦合度。由此可见，其实设计模式就是从大型软件架构出发、便于升级和维护的软件设计思想，它强调降低依赖，降低耦合。

##### 5、迪米特法则，又称最少知道原则（Demeter Principle）

最少知道原则是指：一个实体应当尽量少地与其他实体之间发生相互作用，使得系统功能模块相对独立。

##### 6、合成复用原则（Composite Reuse Principle）

合成复用原则是指：尽量使用合成/聚合的方式，而不是使用继承。


总结：
开闭原则：实现热插拔，提高扩展性。

里氏代换原则：实现抽象的规范，实现子父类互相替换；

依赖倒转原则：针对接口编程，实现开闭原则的基础；

接口隔离原则：降低耦合度，接口单独设计，互相隔离；

迪米特法则，又称不知道原则：功能模块尽量独立；

合成复用原则：尽量使用聚合，组合，而不是继承；



1. 单例模式　
[单例模式](https://github.com/musejianglan/Wiki_Note/blob/master/Design_pattern/singleton（单例模式）.md)
2. 工厂方法模式　
3. 抽象工厂模式　
4. 模版方法模式
[模版方法模式](https://github.com/musejianglan/Wiki_Note/blob/master/Design_pattern/Template(模板模式).md)　
5. 建造者模式　
6. 代理模式　
7. 原型模式　
8. 中介者模式　
9. 命令模式　
10. 责任链模式　
11. 装饰模式　
12. 策略模式　
13. 适配器模式　
14. 迭代器模式　
15. 组合模式　
16. 观察者模式　
17. 门面模式　
18. 备忘录模式　
19. 访问者模式　
20. 状态模式　
21. 解释器模式　
22. 享元模式　
23. 桥梁模式








