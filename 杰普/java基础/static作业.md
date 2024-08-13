1.静态成员变量、静态方法、静态代码块

2.静态成员变量和非静态成员变量的区别(s/uns)

```
1.存储位置：static在方法区的静态存储区，而非static在堆内存里的所属的对象的独立存储空间
2.生命周期：s类加载创建，类卸载销毁。uns对象创建时加载，对象回收时销毁
3.出现顺序，从2可知，s先于uns
4.调用方式：s类名调用，uns对象名调用
5。初始化时期：s类加载，uns对象创建
6，内存占用：看1，s不独立，uns独立空间
7；共享：s共享，uns不共享
```

3.不需要访问对象实例的经常用，比如工具类

4.代码块是创建实例的时候执行，静态代码块只有在类加载时会执行

5.static可以继承，但是不能重写，但是。。。如果定义了同名的static成员，那么父类的静态成员会在子类中隐藏

6.输出结果

```
test static 1
test static 2
代码块
构造器
info
```

```
静态代码块Parent
静态代码块Child
构造代码块Parent
构造方法Parent
构造代码块Child
构造方法Child    就是先静态后其他，然后都是先父，联系类加载的过程来记忆
```

```
静态块
构造块
构造块
构造块
```

7.一个类只有一个实例，并有一个全局访问点

```java
class Singleton {
    private static Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}

```

8.

```java
class Counter {
    private static int count = 0;

    public Counter() {
        count++;
    }

    public static int getCount() {
        return count;
    }

    public static void main(String[] args) {
        new Counter();
        new Counter();
        System.out.println("Instance count: " + Counter.getCount());
    }
}

```

