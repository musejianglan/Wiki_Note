# 简单工厂模式

每次增加一个产品时，都需要增加一个具体类和对象实现工厂，使得系统中类的个数成倍增加，在一定程度上增加了系统的复杂度，同时也增加了系统具体类的依赖。这并不是什么好事。

```
产品类
abstract class BMW {  
    public BMW(){  
          
    }  
}  
  
public class BMW320 extends BMW {  
    public BMW320() {  
        System.out.println("制造-->BMW320");  
    }  
}  
public class BMW523 extends BMW{  
    public BMW523(){  
        System.out.println("制造-->BMW523");  
    }  
}  


工厂类
public class Factory {  
    public BMW createBMW(int type) {  
        switch (type) {  
          
        case 320:  
            return new BMW320();  
  
        case 523:  
            return new BMW523();  
  
        default:  
            break;  
        }  
        return null;  
    }  
}  


客户类
Factory factory = new Factory();  
BMW bmw320 = factory.createBMW(320);  
BMW bmw523 = factory.createBMW(523);  

```


### 工厂方法模式

```
	产品
	interface IProduct {
        public void productMethod();
    }

    class Product implements IProduct {
        public void productMethod() {
            System.out.println("产品");
        }
    }

	class Product2 implements IProduct {
        public void productMethod2() {
            System.out.println("产品2");
        }
    }
    
	工厂
    interface IFactory {
        public IProduct createProduct();
    }

    class Factory implements IFactory {
        public IProduct createProduct() {
            return new Product();
        }
    }
    
    class Factory2 implements IFactory {
        public IProduct createProduct() {
            return new Product2();
        }
    }

    public class Client {
        public static void main(String[] args) {
            IFactory factory = new Factory();
            IProduct prodect = factory.createProduct();
            prodect.productMethod();
        }
    }

```