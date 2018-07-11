## 继承
1.作用：提高了代码的复用性
```
public class animal{
    String eye;
    
    public void run(){
        System.out.println("跑跑");
    }
    
    public void eat(){
        System.out.println("吃吃");
    }
}

class Mammal extends Animal{
    public void taisheng(){
        System.out.println("我是胎生");
    }
}

class Bird extends Animal{
    public void eggsheng(){
        System.out.println("我是卵生");
    }
}
```

## 重写(override)
* 在子类中可以根据需要对从基类中继承来的方法进行重写。
* 重写方法必须和被重写方法具有**相同方法名称、参数列表和返回类型**
* 重写方法不能使用比被重写方法更严格的访问权限。(由于多态)

## Object类
* Object类是所有Java类的根基类
* 如果在类的声明中未使用extends关键字指明其基类，则默认基类为Object类

## super关键字
* super是直接父类对象的引用。可以通过super来访问父类中被子类覆盖的方法或属性。
* 普通方法：没有顺序限制。可以随便调用。
* 任何类的构造函数中，若是构造函数的第一行代码没有显式的调用super();那么Java默认都会调用super();作为父类的初始化函数。所以你这里的super();加不加都无所谓。

## final关键字
* 修饰变量：常量
* 修饰方法：该方法不可被子类重写。但是可以被重载。
* 修饰类：修饰的类不能有子类，不能被继承。比如：Math、String

## 封装
* 隐藏对象内部的复杂性，只对外公开简单的接口。便于外界调用，从而提高系统的可扩展性、可维护性。


修饰符  | 同一个类 | 同一个包 |  子类  |所有类
   ---   |    ---   |    ---   |   ---  |  ---
private    | * |
default    | * | * |   |
protected  | * | * | * |
public     | * | * | * | * |

* 多态存在要有三个必要条件
>要有继承、要有方法重写、父类引用指向子类对象


