##### 数据类型

1.基本数据类型和引用数据类型的区别

2.基本数据类型的各个类型对应的范围（判断）

3.基本数据类型从小到大排序

```
byte->short->int->long
```

4.隐式类型转换

```
+= 是算数符  s=s+1是重新赋值  
+= <--> （左边的类型）s+1  比如 s+=1 == s=(short)(s+1) 如果是s=s+1 这时候先是右边s+1变成了int类型（转换了），然后赋值给左边的short，只能低到高不能高到低，就会精度丢失错误
```

##### 面向对象

1.成员变量在堆内存，全局变量在栈内存

2.谁调用this，this就是谁

3.在构造方法里面，可以在用this(参数)来实现构造方法内调用构造方法，可以用来设置默认值，前提是，<u>**this必须是构造方法内的第一行有效代码**</u>

4.<u>静态方法和成员方法的最大区别就是静态方法里面没有this</u>，但是要使用成员变量的时候内部是用了this的，所以静态方法无法访问成员方法

5.static代码块里的变量只能在定义后初始化赋值

```
static{
		libraty = "123";
}

```

##### //TODO Scanner相关的



##### 关于继承里的

1.super在构造方法里面必须是第一行，因为类的初始化顺序是这样的。子类初始化时<u>**java强制要求了显式或隐式加载父类的无参构造方法【也就是说有参必须要显式调用super】**</u>

（这里可以联系那个java基础面试题里面的类加载的知识一起理解）

```
父类静态变量和静态初始代码块-->子类静态变量和静态初始代码块-->父类实例变量和实例初始代码块-->父类的构造方法加载-->
子类实例变量和实例初始代码块（因为有的是从父类继承过来的）-->子类的构造方法加载
```

因为子类构造方法里可能有依赖父类初始化后的变量和方法，如果不是第一行会报错:

```java
Constructor call must be the first statement in a constructor
```

2.关于访问级别

<img src="/Users/elfish/Library/Application Support/typora-user-images/image-20240731093239711.png" alt="image-20240731093239711" style="zoom:67%;" />



其他没啥，就是protected和默认，举个例子

```java
package com.lyk.A
class parent{
  int defaultfield =10;
  protected protectedfield = 20;
}

package com.lyk.B
class son extends com.lyk.A.parent{
  void getdefault(){
    sout(defaultfield);    //报错，因为默认级别不能跨包访问，即使是子类
  }
  
   void getprotected(){
		sout(protectedfield)   //可以访问到
  }
}
```

##### tostring

//当输出对象时，默认输出的是:对象.toString()

```java
Teacher t = new Teacher();
sout t ;
sout t.toString() ;   //这两个输出是一样的
```

默认输出是符号“@”以及对象的哈希码的无符号十六进制表示

##### 多态

```java
Parent p = new son("lisi",18);
p.work();  //输出结果：上学
```

用处就是可拓展性，代码灵活性

```
//不用的时候
class Game{
	public void play(BasketBall baskertball){sout playxxxxx}
	public void play(footBall football){sout playxxxxx}
	public void play(tennisBall tennisball){sout playxxxxx}
}
//用的时候
//直接弄一个Ball类，其他的都继承自他
class Game{
public void play(Ball ball){ball.play}  //这里的参数可以直接随便传子类的对象，最直观的就是不用每个类都写一次方法了
}
```

##### 多态里的类型转换

```java
Parent Son1 Son2
Parent a = new Son1（）;  //这里叫做向上转换（是右边相对左边说的）
Son1 b = (Son1)a;   //这个就是向下转换，前提是必须有前面的向上转换
//重点⚠️：这里的a无法访问到Son1里的非继承的成员变量和方法
Son2 c = (Son2)a;   //这里会报错的，因为a是Son1转换的Parent，所以不能强转成Son2
那么怎么判断一个 a 他是Son1 还是Son2 转换来的呢，用 【instanceof】方法，返回值是boolean
a instanceof Son1;  //true
```

##### 抽象类，接口

1.抽象类的子类也可以是抽象类，就是不完全重写抽象方法的结果。

2.接口里的方法其实就是隐式的抽象方法

```java
public interface it1{
//abstract void func1();
  void func1();  //这里这两个一模一样
}
```

但是因为接口为了所有实现类遵守契约，所以必须完全重写接口里面的方法，而不是像上面的第1点。

3.JDK8之后接口内可以有default方法和静态方法，也可以定义常量

```java
public interface it1{
	//public static final String a = "hello"
	 String a = "hello";//这两行一模一样
}
```

##### 代码块

```java
class myClass{
{sout("正在创建对象")}
}
```

如上所见，作用是每创建对象的时候运行一遍

比构建方法先运行

##### static可以继承

、，但是不能重写，但是。。。如果定义了同名的static成员，那么父类的静态成员会在子类中隐藏

##### static资源加载之前，可以加载构造方法

例子

```java
class B {
    public static B b = new B();
    public static B b2 = new B();

    {
        System.out.println("构造块");
    }

    static {
        System.out.println("静态块");
    }
}

public class Test06 {
    public static void main(String[] args) {
        B b = new B();
    }
}

```

```
输出结果
构造块
构造块
静态块
构造块
```

##### 单例模式

单例模式是一种设计模式，旨在确保一个类只有一个实例，并提供一个全局访问点。这种模式在以下情况下特别有用：

1. **控制资源使用**：如数据库连接池、线程池、配置文件读取器等，确保资源的唯一性和有效管理。
2. **全局状态管理**：在应用程序中，某些组件需要共享状态或配置，使用单例模式可以方便地管理这些全局状态。
3. **性能优化**：减少实例化开销，避免重复创建对象，提高系统性能。
4. **避免冲突**：确保系统中某些关键部分只有一个实例，避免多实例带来的冲突和不一致性问题。

##### String常量池 `.intern()`

String a ="123";

String b =new String("123").intern();

sout(a==b);    true

这个方法是先去池里看是否有，有直接拿来他的引用地址
