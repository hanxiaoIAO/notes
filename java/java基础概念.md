## 什么是java虚拟机？为什么java被称作是“与平台无关的编程语言”？

​	Java虚拟机是一个可以执行Java字节码的虚拟机进程。Java源文件被编译成能被Java虚拟机执行的字节码文件。

​	Java被设计成允许应用程序可以运行在任意的平台，而不需要程序员为每一个平台单独重写或重新编译。Java虚拟机让这个变为可能，因为它知道底层硬件平台的指令长度和其他特性。

## JDK、JRE、JVM

​	JDK(Java Development Kit)即为Java开发工具包，包含编写Java程序所必须的编译、运行等开发工具以及JRE。开发工具如：用于编译Java程序的javac命令、用于启动JVM运行java程序的java命令、用于生成文档的javadoc命令以及用于打包的jar命令等等。

​	JRE(Java Runtime Environment)即为Java运行环境，提供运行java应用程序所必须的软件环境，包含Java虚拟机(JVM)和丰富的系统类库。系统类库即为java提前封装好的功能类，只需拿来直接使用即可，可以大大的提高开发效率。

​	JVM(Java Virtual Mahines)即为Java虚拟机，提供字节码文件(.class)的运行环境支持。

​	简单的说，就是JDK包含JRE包含JVM。

## 面对对象的四大基本特性

抽象：提取现实世界中某事物的关键特性，为该事物构建模型的过程。对同一事物在不同的需求下，需要提取的特性可能不一样。得到的抽象模型中一般包含：属性(数据)和操作(行为)。这个抽象模型我们称之为类。对类进行实例化得到对象。

封装：封装可以是类具有独立性和隔离性；保证类的高内聚。只暴露给类外部或者子类必须的属性和操作。类封装的实现依赖类的修饰符(public、protected和private等)

继承：对现有类的一种复用机制。一个类如果继承现有的类，则这个类将拥有被继承类的所有非私有特性(属性和操作)。这里指的继承包含：类的继承和接口的实现。

多态：多态是在继承的基础上实现的。多态的是哪个要素：继承、重写和父类引用指向子类对象。父类引用指向不同的子类对象时，调用相同的方法，呈现不同的行为。就是类多态特性。多态可以分为编译时多态和运行时多态。

## 重写和重载

重载：方法名称一致,但是参数个数,参数类型,参数顺序不一致

重写：重写存在子类继承父类中,其中子类定义一个方法,该方法的方法名,参数,类型都跟父类一致

## 七大设计原则

抽象、封装、继承和多态是面对对象的基础。在面对对象的四大基础特性之上，我们在做面向对象编程设计师还需遵循一些基本的设计原则。

SOLID原则(单一职责原则、开放关闭原则、里氏替换原则、接口隔离原则和依赖倒置原则)

迪米特法则

组合优于继承原则(合成复用原则)