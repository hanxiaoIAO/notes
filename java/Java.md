[TOC]



## 概念

### 4.24中设计模式(gof23+1)

- 1. 简单工厂模式(不包含在gof23中)

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

### 10.解释内存中的栈(stack)、堆(heap)和方法区(method area)的用法

​	通常我们定义一个基本数据类型的变量，一个对象的引用，还有就是函数调用的现场保存都使用JVM中的栈空间；而通过new关键字和构造器创建的对象则放在堆空间，栈是垃圾收集器管理的主要区域，由于现在的垃圾收集器都采用分代收集算法，所以堆空间还可以细分为新生代和老生代，再具体一点可以分为Eden，Survivor(又可分为From Survivor和To Survivor)、Tenured。方法区和堆都是各个线程共享的内存区域，用于存储已经被JVM加载的类信息、常量、静态变量、JIT编译器编译后的代码等数据；程序中的字面量(literal)如直接书写的100、"hello"和常量都是放在常量池中，常量池是方法区的一部分。栈空间操作起来最快但是栈最小，通常大量的对象都是放在堆空间，栈和堆的大小都可以通过JVM的启动参数来进行调整，栈用光了会引发StackOverflowError，而堆和常量池空间不足则会引发OutOfMemoryError.

### 12.手写单例模式（饿汉模式和饱汉模式），工厂模式

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

