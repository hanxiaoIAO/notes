[TOC]



# Java

## 接口和抽象类的差别

设计层面：

- 抽象类是对整个类整体进行抽象，包括属性、行为，但是接口却是对类局部（行为）进行抽象。

语法：

- 接口中的所有方法隐含的都是抽象的。而抽象类则可以同时包含抽象和非抽象的方法。
- 类可以实现多个接口，但是只能继承一个抽象类。接口可以继承多个接口。
- 接口中不能含有静态代码块以及静态方法，而抽象类可以有静态代码块和静态方法。
- 抽象类中的成员变量可以是各种类型的，而接口中的成员变量只能是public static final类型的。

## 数据类型

​	基本数据类型：

​	整数值型：

​			byte：数据类型是8位、有符号的，以二进制补码表示的整数。(-128~127）二字节

​			short:数据类型是 16 位、有符号的以二进制补码表示的整数。(-32768~32767) 四字节

​			int:数据类型是32位、有符号的以二进制补码表示的整数。八字节

​			long:数据类型是 64 位、有符号的以二进制补码表示的整数。十六字节

​	字符型：char 八字节

​	浮点型：

​			float: 八字节

​			double: 十六字节

​	布尔型：boolean

​	枚举类型：enmu

​	整数默认int型，小数默认double型。float和long类型的必须加后缀。

​	首先知道String是引用类型，自动装箱和拆箱就是基本类型和引用类型之间的转换。基本类型转换为引用类型之后，就可以new对象，从而调用包装类中封装好的方法进行基本类型之间的转换或者toString(当然用类名直接调用也可以，便于一眼看出该方法是静态的)，还有就是如果集合中想存放基本类型，泛型的限定类只能是对应的包装类型。



```java
public class TestEnum
{
    public enum Color
    {
        RED("红色",1),GREEN("绿色",2),WHITE("白色",3),YELLOW("黄色",4);
        //成员变量
        private String name;
        private int index;
        //构造方法
        private Color(String name,int index)
        {
            this.name=name;
            this.index=index;
        }
        //覆盖方法
        @Override
        public String toString()
        {
            return this.index+"-"+this.name;
        }
    }
    public static void main(String[] args)
    {
        System.out.println(Color.RED.toString());    //输出：1-红色
    }
}
```



## 异常

　　Java异常是Java提供的一种识别及响应错误的一致性机制。

### 关键字

​		Java异常机制用到的几个关键字：**try、catch、finally、throw、throws。**

• **try**        -- 用于监听。将要被监听的代码(可能抛出异常的代码)放在try语句块之内，当try语句块内发生异常时，异常就被抛出。
• **catch**   -- 用于捕获异常。catch用来捕获try语句块中发生的异常。
• **finally**  -- finally语句块总是会被执行。它主要用于回收在try块里打开的物力资源(如数据库连接、网络连接和磁盘文件)。只有finally块，执行完成之后，才会回来执行try或者catch块中的return或者throw语句，如果finally中使用了return或者throw等终止方法的语句，则就不会跳回执行，直接停止。
• **throw**   -- 用于抛出异常。
• **throws** -- 用在方法签名中，用于声明该方法可能抛出的异常。

### java异常框架

1. Throwable
　　Throwable是 Java 语言中所有错误或异常的超类。
Throwable包含两个子类: **Error** 和 **Exception**。它们通常用于指示发生了异常情况。
Throwable包含了其线程创建时线程执行堆栈的快照，它提供了printStackTrace()等接口用于获取堆栈跟踪数据等信息。

2. Exception
　　Exception及其子类是 Throwable 的一种形式，它指出了合理的应用程序想要捕获的条件。

3. Error
   
   和Exception一样，Error也是Throwable的子类。它用于指示合理的应用程序不应该试图捕获的严重问题，大多数这样的错误都是异常条件。编译器也不会检查Error。
   
   当资源不足、约束失败、或是其它程序无法继续运行的条件发生时，就产生错误。程序本身无法修复这些错误的。
   
4. RuntimeException
   　　Exception的子类。RuntimeException是那些可能在 Java 虚拟机正常运行期间抛出的异常的超类。
   编译器不会检查RuntimeException异常。
   如果代码会产生RuntimeException异常，则需要通过修改代码进行避免。例如，若会发生除数为零的情况，则需要通过代码避免该情况的发生！
   
5. 被检查的异常

     Exception类本身，以及Exception的子类中除了"运行时异常"之外的其它子类都属于被检查异常。

     Java编译器会检查它。此类异常，要么通过throws进行声明抛出，要么通过try-catch进行捕获处理，否则不能通过编译。





## 概念

### 1.什么是java虚拟机？为什么java被称作是“与平台无关的编程语言”？

​	Java虚拟机是一个可以执行Java字节码的虚拟机进程。Java源文件被编译成能被Java虚拟机执行的字节码文件。

​	Java被设计成允许应用程序可以运行在任意的平台，而不需要程序员为每一个平台单独重写或重新编译。Java虚拟机让这个变为可能，因为它知道底层硬件平台的指令长度和其他特性。

### 2.JDK、JRE、JVM

​	JDK(Java Development Kit)即为Java开发工具包，包含编写Java程序所必须的编译、运行等开发工具以及JRE。开发工具如：用于编译Java程序的javac命令、用于启动JVM运行java程序的java命令、用于生成文档的javadoc命令以及用于打包的jar命令等等。

​	JRE(Java Runtime Environment)即为Java运行环境，提供运行java应用程序所必须的软件环境，包含Java虚拟机(JVM)和丰富的系统类库。系统类库即为java提前封装好的功能类，只需拿来直接使用即可，可以大大的提高开发效率。

​	JVM(Java Virtual Mahines)即为Java虚拟机，提供字节码文件(.class)的运行环境支持。

​	简单的说，就是JDK包含JRE包含JVM。

### 3.Java支持的数据类型有哪些？什么是自动拆装箱？

​	基本数据类型：

​	整数值型：byte，short，int，long

​	字符型：char

​	浮点型：float,double

​	布尔型：boolean

​	整数默认int型，小数默认double型。float和long类型的必须加后缀。

​	首先知道String是引用类型，自动装箱和拆箱就是基本类型和引用类型之间的转换。基本类型转换为引用类型之后，就可以new对象，从而调用包装类中封装好的方法进行基本类型之间的转换或者toString(当然用类名直接调用也可以，便于一眼看出该方法是静态的)，还有就是如果集合中想存放基本类型，泛型的限定类只能是对应的包装类型。

### 4.面对对象是什么？

​	面想对象是一种思想，世间万物都可以看做一个对象，这里只讨论面向对象编程（OOP）,Java是一个支持高并发、基于类和面向代码开发模块化，更容易维护和修改；

​	代码复用性强；

​	增强代码的可靠性和灵活性；

​	增加代码的可读性；

- 面对对象的四大基本特性：

  抽象：提取现实世界中某事物的关键特性，为该事物构建模型的过程。对同一事物在不同的需求下，需要提取的特性可能不一样。得到的抽象模型中一般包含：属性(数据)和操作(行为)。这个抽象模型我们称之为类。对类进行实例化得到对象。

  封装：封装可以是类具有独立性和隔离性；保证类的高内聚。只暴露给类外部或者子类必须的属性和操作。类封装的实现依赖类的修饰符(public、protected和private等)

  继承：对现有类的一种复用机制。一个类如果继承现有的类，则这个类将拥有被继承类的所有非私有特性(属性和操作)。这里指的继承包含：类的继承和接口的实现。

  多态：多态是在继承的基础上实现的。多态的是哪个要素：继承、重写和父类引用指向子类对象。父类引用指向不同的子类对象时，调用相同的方法，呈现不同的行为。就是类多态特性。多态可以分为编译时多态和运行时多态。



​	抽象、封装、继承和多态是面对对象的基础。在面对对象的四大基础特性之上，我们在做面向对象编程设计师还需遵循一些基本的设计原则。

- 面对对象的七大设计原则

  SOLID原则(单一职责原则、开放关闭原则、里氏替换原则、接口隔离原则和依赖倒置原则)

  迪米特法则

  组合优于继承原则(合成复用原则)

- 24中设计模式(gof23+1)

  1. 简单工厂模式(不包含在gof23中)

  2. 工厂模式

  3. 抽象工厂模式

  4. 单例模式

  5. 原型模式

     创建者模式：

  6. 结构型模式

  7. 组合模式

  8. 装饰者模式

  9. 外观模式

  10. 适配器模式

  11. 代理模式

  12. 享元模式

  13. 桥接模式

      行为型模式：

  14. 观察者模式

  15. 策略模式

  16. 状态模式

  17. 中介模式

  18. 模板模式

  19. 命令模式

  20. 备忘录模式

  21. 访问者模式

  22. 解释器模式

  23. 迭代器模式

  24. 职责链模式



### 5.值传递和引用传递

​	值传递是对基本型变量而言，传递的事该变量的一个副本，改变副本不影响原变量。

​	引用传递一般是对于对象型变量而言的，传递的是该对象地址的一个副本，并不是原对象本身。

​	一般认为java内传递的都是值传递，java实例对象的传递是引用传递。

### 6.是否可以在static环境中访问非static变量？

​	static变量在java中是属于类的，它在所有的实例中的值是一样的。当类被Java虚拟机载入时，会对static变量进行初始化。如果你的代码尝试不用实例来访问非static的变量，编译器会报错，因为这些变量还没有被创建出来，还没有跟任何实例关联上。

### 7.Java中的方法覆盖(Overriding)和方法重载(Overloading)是什么意思？

​	Java中的方法重载发生在同一个类里面两个或者多个方法名相同，但是参数不同的情况。与此相对，方法覆盖是说子类重新定义了父类的方法。

​	方法覆盖必须有相同的方法名，参数列表和返回类型。覆盖者可能不会限制它所覆盖的方法的访问。

### 8.Java中，什么是构造方法？什么是构造方法重载？什么是复制的构造方法？

​	当新对象被创建的时候，构造函数会被调用。每一个类都有构造函数。在程序员没有给类提供构造方法的情况下，Java编译器会为这个类创建一个默认的构造方法。

​	Java中构造方法的重载和方法的重载很相似。可以为一个类创建多个构造方法。每一个构造方法必须有他唯一的参数列表。

​	Java不支持像C++中那样的复制构造方法，这个不同点是因为如果你不自己写构造方法的情况下，Java不会创建默认的复制构造方法。

### 9.Java支持多继承吗？

​	Java中类不支持多继承，只支持单继承(即一个类只有一个父类)。但是java中的接口支持多继承，即一个子接口有多个父接口。(接口的作用是用来扩展对象的功能，一个子接口继承多个父接口，说明子接口扩展了多个功能，当类实现接口时，类就扩展了相应的功能)。

### 10.解释内存中的栈(stack)、堆(heap)和方法区(method area)的用法

​	通常我们定义一个基本数据类型的变量，一个对象的引用，还有就是函数调用的现场保存都使用JVM中的栈空间；而通过new关键字和构造器创建的对象则放在堆空间，栈是垃圾收集器管理的主要区域，由于现在的垃圾收集器都采用分代收集算法，所以堆空间还可以细分为新生代和老生代，再具体一点可以分为Eden，Survivor(又可分为From Survivor和To Survivor)、Tenured。方法区和堆都是各个线程共享的内存区域，用于存储已经被JVM加载的类信息、常量、静态变量、JIT编译器编译后的代码等数据；程序中的字面量(literal)如直接书写的100、"hello"和常量都是放在常量池中，常量池是方法区的一部分。栈空间操作起来最快但是栈最小，通常大量的对象都是放在堆空间，栈和堆的大小都可以通过JVM的启动参数来进行调整，栈用光了会引发StackOverflowError，而堆和常量池空间不足则会引发OutOfMemoryError.

### 11.接口和抽象类的区别是什么？

​	从设计层面来说，抽象是对类的抽象，是一种模板设计，接口是对行为的抽象，是一种行为的规范。

​	Java提供和支持创建抽象类和接口。

​	接口中的所有方法隐含的都是抽象的。而抽象类则可以同时包含抽象和非抽象的方法。

​	类可以实现多个接口，但是只能继承一个抽象类。

​	类可以不实现抽象类和接口声明的所有方法，当然，在这种情况下，类也必须得声明成是抽象的。

​	抽象类可以在不提供接口方法实现的情况下实现接口。

​	Java接口中声明的变量默认都是final的。抽象类可以包含非final的变量。

​	Java接口中的成员函数默认是public的。抽象类的成员函数可以是private，protected或者是public。

​	接口是绝对抽象的，不可以被实例化的。抽象类也不可以被实例化，但是，如果它包含main方法的话是可以被调用的。

### 12.手写单例模式（饿汉模式和饱汉模式），工厂模式

### 13.String和StringBuilder、StringBuffer的区别

​	Java平台提供了两种类型的字符串：String和StringBuffer/StringBuilder,它们可以储存和操作字符串。其中String是只读字符串，也就意味着String引用的字符串内容是不能被改变的。而StringBuffer/StringBuilder类表示的字符串对象可以直接进行修改。StringBuilder是Java5中引入的，它和StringBuffer的方法完全相同，区别在于它是在单线程环境下使用的，因为它的所有方面都没有被synchronized修饰，因此它的效率也比StringBuffer要高。

### 14.Java集合框架是什么？说出一些集合框架的优点？

​	每种编程语言中都有集合，最初的Java版本包含几种集合类：Ventor、Stack、HashTable和Array。随着集合的广泛使用，Java1.2提出了囊括所有集合接口、实现和算法的集合框架。在保证线程安全的情况下使用泛型和并发集合类，Java已经经历了很久。它还包括在Java并发包中，阻塞接口以及它们的实现。集合框架的部分优点如下：

（1）使用核心集合类降低开发成本，而非实现我们的集合类。

（2）随着使用经过严格测试的集合框架类，代码质量会得到提高。

（3）通过使用JDK附带的集合类，可以降低代码维护成本。

（4）复用性和可操作性。

### 15.集合框架中的泛型中有什么优点？

​	Java1.5引入了泛型，所有的集合接口和实现都大量的使用它。泛型允许我们为集合提供一个可以容纳的对象类型，因此，如果你添加其他类型的任何元素，它会在编译时报错。这避免了在运行时出现ClassCastExcepption,因为你将会在编译时得到报错信息。泛型也使得代码整洁，我们不需要使用显式转换和instanceOf操作符。它也给运行时带来好处，因为不会产生类型检查的字节码指令。

### 16.Java集合框架的基础接口有哪些？

​	Collection为集合层级的根接口。一个集合代表一组对象，这些对象即为它的元素。Java平台不提供这个接口任何直接的实现。

​	Set是一个不能包含重复元素的集合。这个接口对数学集合抽象进行建模，被用来代表集合，就如一副牌。

​	List是一个有序集合，可以包含重复元素。你可以通过它的索引类访问任何元素。List更像长度动态变换的数组。

​	Map是一个将key映射到value的对象。一个Map不能包含重复的key:每个key最多只能映射一个value。

​	其他的接口还有Queue、Dequeue、SortedSet、SortedMap和ListIterator。

### 17.为何Collection不从Cloneable和Serializable接口继承？

​	Collection接口指定一组对象，对象即为它的元素。如何维护这些元素有Collection的具体实现决定。例如，一些如List的Collection实现允许重复的元素，而其他的如Set就不允许。很多Collection实现由一个共有的clone方法。然而，把它放到集合的所有实现中也是没有意义的。这是因为Collection是一个抽象表现。重要的事实现。

​	当与具体实现打交道的时候，克隆或序列化的语义和含义才发挥作用。所以，具体实现应该决定如何对它进行克隆或序列化，或它是否可以被克隆或序列化。

​	在所有的实现中授权克隆和序列化，最终导致更少的灵活和更多的限制。特定的实现应该决定如何对它进行克隆或序列化。

### 18.为何Map接口不继承Collection接口？

​	尽管Map接口和它的实现也是集合框架的一部分，但Map不是集合，集合也不是Map。因此，Map继承Collection毫无意义，反之亦然。

​	如果Map继承Collection接口，那么元素去哪儿？Map包含Key-Value列表集合的方法，但是它不适合“一组对象”规范。

### 19.什么是迭代器(Iterator)?

​	Iterator接口提供了很多对集合元素进行迭代的方法。每一个集合类都包含了可以返回迭代器实例的迭代方法。迭代器可以在迭代的过程中删除底层集合的元素，但是不可以直接调用集合的remove(Object obj)删除，可以通过迭代器的remove()方法删除。

### 20.Iterator和ListIterator的区别是什么？

​	Iterator可用来遍历Set和List集合，但是ListIterator只能用来遍历List。

​	Iterator对集合只能是前向遍历，ListIterator既可以前向也可以后向。

​	ListIterator实现了Iterator接口，并包含其他的功能，比如：增加元素，替换元素，获得前一个和后一个元素的索引等等。

### 21.快速失败(fail-fast)和安全失败(fail-safe)的区别是什么？

​	快速失败：当你在迭代一个集合的时候，如果有另一个线程正在修改你正在访问的那个集合，就会跑出一个ConcurrentModification异常。

​	在java.util包下的都是快速失败。

​	安全失败：在迭代的时候会去底层集合做一个拷贝，所以你在修改上层集合的时候是不会受到影响的，不会抛出ConcurrentModification异常。

​	在java.util.concurrent包下的全是安全失败的。

### 22.Java中的HashMap的工作原理是什么？

​	我们知道在java中最长用的两种结构是数组和模拟指针(引用)，几乎所有的数据结构都可以利用这两种组合来实现，HashMap也是如此。实际上HashMap是一个"链表散列"，如下是它数据结构：最左侧是一个数组，数组中的每一个元素都是一个链表，链表的每一个元素都是entry。

​	HashMap是基于hashing的原理，我们使用put(key,value)存储对象到HashMap中，使用get(key)从HashMap中获取对象。当我们给put()方法传递键和值时，我们先对键调用hashCode()方法，返回的hashCode用于找到bucket位置来存储Entry对象。

### 23.当两个对象的hashcode相同会发生什么？

​	因为hashcode相同，所以他们的bucket位置相同，‘碰撞’会发生。因为HashMap使用链表存储对象，这个Entry(包含有键值对的Map.Entry对象)会存储在链表中。

### 24.如果两个键的HashCode相同，你如何获取值对象？

​	当我们调用get()方法，HashMap会使用键对象的hashcode找到bucket位置，然后调用keys.equals()方法区找到链表中正确的节点，最终找到要找的值对象。

### 25.hashcode()和equals()方法有何重要性？

​	HashMap使用Key对象的hashcode()和equals()方法去决定key-value对的索引。当我们试着从HashMap中获取值得时候，这些方法也会被用到。如果这些方法没有被正确地实现，在这种情况下，两个不同Key也许会产生相同的hashcode()和equals()输出，HashMap将会认为它们是相同的，然后覆盖它们，而非把它们存储到不同的地方。同样的，所有不允许存储重复数据的集合类都使用hashCode()和equals()去查找重复，所以正确实现它们非常重要。equals()和hashCode()的实现应该遵循以下规则：

​	(1) 如果o1.equals(o2),那么o1.hashCode() == o2.hashCode()总是true的。

​	(2)如果o1.hashCode() == o2.hashCode(),并不意味着o1.equals(o2)会是true。

### 26.HashMap和HashTable有什么区别？

1. HashMap是非线程安全的，HashTable是线程安全的。
2. HashMap的键和值都允许有null值存在，而HashTable则不行。
3. 因为线程安全的问题，HashMap效率比HashTable的要高。
4. HashTable是同步的，而HashMap不是。因此，HashMap更适合于单线程环境，而HashTable适合于多线程环境。

​	一般不建议用HashTable。HashTable是遗留类，内部实现很多没优化和冗余。即使在多线程环境下，现在也有同步的ConcurrentHashMap替代，没有必要时因为多线程而用HashTable。

### 27.如何决定选用HashMap还是TreeMap?

​	对于在Map中插入、删除和定位元素这类操作，HashMap是最好的选择。然而，假如你需要对一个有序的Key集合进行遍历，TreeMap是更好的选择。基于你的collection的大小，也许想HashMap中添加元素会更快，将map换为TreeMap进行有序Key的遍历。

### 28.ArrayList和Vector有何异同点

​	ArrayList和Vector在很多时候都很类似。

1. 两者都是基于索引的，内部由一个数组支持。

2. 两者维护插入的顺序，我们可以根据插入顺序来获取元素。

3. ArrayList和Vector的迭代器实现都是fail-fast的。

4. ArrayList和Vector两者允许null值，也可以使用索引值对元素进行随机访问。

   以下是ArrayList和Vector的不同点。

5. Vector是同步的，而ArrayList不是。然而，如果你寻求在迭代的时候对列表进行改变，，你应该使用CopyOnWriteArrayList。

6. ArrayList比Vector快，它因为有同步，不会过载。

7. ArrayList更加通用，因为我们可以使用Collections工具类轻易地获取同步列表和只读列表

### 29.Array和ArrayList有何区别？

​	Array可以容纳基本类型和对象，而ArrayList只能容纳对象。

​	Array是指定大小的，而ArrayList大小是固定的。

​	Array没有提供ArrayList那么多功能，比如addAll、removeAll和Iterator等。尽管ArrayList明显是更好的选择，但也有些时候Array比较好用。



# 

GOF设计模式
Java 中Timer和TimerTask 定时器和定时任务使用

2.
文件

	File file = new File("" + ".xml");
	FileUtils.writeStringToFile(file, sb.toString(), "UTF-8");

3.
判断是否为中文
   static String regEx = "[\u4e00-\u9fa5]";
   static Pattern pat = Pattern.compile(regEx);

    public static boolean isContainsChinese(String str) {
    	Matcher matcher = pat.matcher(str);
    	boolean flg = false;
    	if (matcher.find()) {
    		flg = true;
    	}
    	return flg;
    }



1.BigDecimal类型比较数值大小必须使用 public int compareTo(BigDecimal val)方法，返回－１小于，０等于，１大于
2.常用IO流类：FileInputStream和FileOutputStream 
  用于解析xml等类型文件：	org.dom4j.*;

	FileInputStream initDateFile = new FileInputStream(fileName);
	SAXReader saxReader = new SAXReader();
	Document document = saxReader.read(initDateFile);
	
	attribute和Element
3.   以下是java 判断字符串是否为空的四种方法:
    方法一: 最多人使用的一个方法, 直观, 方便, 但效率很低:
     ​                               if(s == null ||"".equals(s));
    方法二: 比较字符串长度, 效率高, 是我知道的最好一个方法:
     ​                 if(s == null || s.length() <= 0);
    方法三: Java SE 6.0 才开始提供的方法, 效率和方法二几乎相等, 但出于兼容性考虑, 推荐使用方法二.
     ​                if(s == null || s.isEmpty());
    方法四: 这是一种比较直观,简便的方法,而且效率也非常的高,与方法二、三的效率差不多:
     ​                if (s == null || s == "");
    
    注意:s == null 是有必要存在的.
　　如果 String 类型为null, 而去进行 equals(String) 或 length() 等操作会抛出java.lang.NullPointerException.
　　并且s==null 的顺序必须出现在前面，不然同样会抛出java.lang.NullPointerException.
4.String s ;该语句表示只是声明了一个引用变量,但是并没有初始化引用,所以对变量s的任何操作(除了初始化赋值外) 都将引发异常.
​    String s=null; 表示未申请任何内存资源，即些语句表示声明了一个引用变量并初始化引用,但是该引用没有指向任何对象.但可以把它作为参数传递或其它使用,但是不能调用它作为对象的方法
​    String s=""; 表示申请了内存资源，但资源空间值为空。该语句表示声明并引用到一个对象,只不过这个对象为0个字节.所以既然有了对象,就可以调用对象的方法
​    注意："" 也是字符串
​    String s = String.Empty 与 String s=""; 是完全相同的 
5.instanceof是Java、php的一个二元操作符（运算符），和==，>，<是同一类东西。由于它是由字母组成的，所以也是Java的保留关键字。它的作用是判断其左边对象是否为其右边类的实例，返回boolean类型的数据。可以用来判断继承中的子类的实例是否为父类的实现。相当于c#中的is操作符。java中的instanceof运算符是用来在运行时指出对象是否是特定类的一个实例。instanceof通过返回一个布尔值来指出，这个对象是否是这个特定类或者是它的子类的一个实例。
6.使用　break continue return　的时候注意范围


GOF设计模式
Java 中Timer和TimerTask 定时器和定时任务使用

2.
文件

	File file = new File("" + ".xml");
	FileUtils.writeStringToFile(file, sb.toString(), "UTF-8");

3.
判断是否为中文
   static String regEx = "[\u4e00-\u9fa5]";
   static Pattern pat = Pattern.compile(regEx);

    public static boolean isContainsChinese(String str) {
    	Matcher matcher = pat.matcher(str);
    	boolean flg = false;
    	if (matcher.find()) {
    		flg = true;
    	}
    	return flg;
    }



1.BigDecimal类型比较数值大小必须使用 public int compareTo(BigDecimal val)方法，返回－１小于，０等于，１大于
2.常用IO流类：FileInputStream和FileOutputStream 
  用于解析xml等类型文件：	org.dom4j.*;

	FileInputStream initDateFile = new FileInputStream(fileName);
	SAXReader saxReader = new SAXReader();
	Document document = saxReader.read(initDateFile);
	
	attribute和Element
3.   以下是java 判断字符串是否为空的四种方法:
    方法一: 最多人使用的一个方法, 直观, 方便, 但效率很低:
     ​                               if(s == null ||"".equals(s));
    方法二: 比较字符串长度, 效率高, 是我知道的最好一个方法:
     ​                 if(s == null || s.length() <= 0);
    方法三: Java SE 6.0 才开始提供的方法, 效率和方法二几乎相等, 但出于兼容性考虑, 推荐使用方法二.
     ​                if(s == null || s.isEmpty());
    方法四: 这是一种比较直观,简便的方法,而且效率也非常的高,与方法二、三的效率差不多:
     ​                if (s == null || s == "");
    
    注意:s == null 是有必要存在的.
　　如果 String 类型为null, 而去进行 equals(String) 或 length() 等操作会抛出java.lang.NullPointerException.
　　并且s==null 的顺序必须出现在前面，不然同样会抛出java.lang.NullPointerException.
4.String s ;该语句表示只是声明了一个引用变量,但是并没有初始化引用,所以对变量s的任何操作(除了初始化赋值外) 都将引发异常.
​    String s=null; 表示未申请任何内存资源，即些语句表示声明了一个引用变量并初始化引用,但是该引用没有指向任何对象.但可以把它作为参数传递或其它使用,但是不能调用它作为对象的方法
​    String s=""; 表示申请了内存资源，但资源空间值为空。该语句表示声明并引用到一个对象,只不过这个对象为0个字节.所以既然有了对象,就可以调用对象的方法
​    注意："" 也是字符串
​    String s = String.Empty 与 String s=""; 是完全相同的 
5.instanceof是Java、php的一个二元操作符（运算符），和==，>，<是同一类东西。由于它是由字母组成的，所以也是Java的保留关键字。它的作用是判断其左边对象是否为其右边类的实例，返回boolean类型的数据。可以用来判断继承中的子类的实例是否为父类的实现。相当于c#中的is操作符。java中的instanceof运算符是用来在运行时指出对象是否是特定类的一个实例。instanceof通过返回一个布尔值来指出，这个对象是否是这个特定类或者是它的子类的一个实例。
6.使用　break continue return　的时候注意范围

