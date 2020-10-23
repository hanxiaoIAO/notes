[toc]

## 关键字

### Java中修饰符的作用域及可见性

| 作用域            | 当前类 | 同一package | 子孙类 | 其他package |
| ----------------- | ------ | ----------- | ------ | ----------- |
| public            | ✔      | ✔           | ✔      | ✔           |
| protected         | ✔      | ✔           | ✔      | ×           |
| default(无修饰符) | ✔      | ✔           | ×      | ×           |
| private           | ✔      | ×           | ×      | ×           |

### abstract

```java
public abstract class MyAbstractClass {
	public void test1(){
   
    } // 一个正常的方法
	public abstract void test2(); // 一个抽象方法。
}
提示，如果JAVA类的任何一个方法是abstract的，则类本身必须是abstract的。
```

### final

final可以修饰变量，方法和类。

修饰变量：

> - 修饰基本数据类型变量时，不能对基本数据类型变量重新赋值，因此基本数据类型变量不能被改变。
> - 修饰引用类型变量时，它仅仅保存的是一个引用，final只保证这个引用类型变量所引用的地址不会发生改变，即一直引用这个对象，但这个对象属性是可以改变的。



> - 修饰类变量（static 修饰的变量）时，必须要在静态初始化块中指定初始值或者声明该类变量时指定初始值，而且只能在这两个地方之一进行指定；
> - 实例变量：必要要在非静态初始化块、声明该实例变量时或者在构造器中指定初始值，而且只能在这三个地方之一进行指定。

修饰方法：

> 父类的final方法是不能够被子类重写的，类的private方法会隐式地被指定为final方法。

修饰类：

> 当一个类被final修饰时，表明该类是不能被子类继承的。

#### 宏变量

利用final变量的不可更改性，在满足一下三个条件时，该变量就会成为一个“宏变量”，即是一个常量。

1. 使用final修饰符修饰；
2. 在定义该final变量时就指定了初始值；
3. 该初始值在编译时就能够唯一指定。

**注意：当程序中其他地方使用该宏变量的地方，编译器会直接替换成该变量的值**

```java
public class Test {
    public static void main(String[] args)  {
        String a = "hello2"; 
        final String b = "hello";
        String d = "hello";
        String c = b + 2; 
        String e = d + 2;
        System.out.println((a == c));
        System.out.println((a == e));
    }
}
	
true
false
```

```java
public class Test {
    public static void main(String[] args)  {
        String a = "hello2"; 
        final String b = getHello();
        String c = b + 2; 
        System.out.println((a == c));
 
    }
 
    public static String getHello() {
        return "hello";
    }
}

false
```

static作用于成员变量用来表示只保存一份副本，而final的作用是用来保证变量不可变

```java
public class Test {
    public static void main(String[] args)  {
        MyClass myClass1 = new MyClass();
        MyClass myClass2 = new MyClass();
        System.out.println(myClass1.i);
        System.out.println(myClass1.j);
        System.out.println(myClass2.i);
        System.out.println(myClass2.j);
 
    }
}
 
class MyClass {
    public final double i = Math.random();
    public static double j = Math.random();
}

i的值是不同的
j的值是相同的
```

#### 匿名内部类中的final

匿名内部类中使用的外部局部变量为什么只能是final变量？

这个问题请参见《Java内部类详解》](http://www.cnblogs.com/dolphin0520/p/3811445.html)

#### 多线程中的final

参见[多线程中final](https://blog.csdn.net/u011521203/article/details/80172121)

### transient

​	Java的serialization提供了一种持久化对象实例的机制。当持久化对象时，可能有一个特殊的对象数据成员，我们不想用serialization机制来保存它。为了在一个特定对象的一个域上关闭serialization，可以在这个域前加上关键字transient。当一个对象被序列化的时候，transient型变量的值不包括在序列化的表示中，然而非transient型的变量是被包括进去的。

### Java异常相关关键字

try、catch、finally、throw、throws。