## 注解定义

Java 注解（Annotation）又称 Java 标注，是 JDK5.0 引入的一种注释机制。

1. 注解是一种元数据形式。
2. 注解用来修饰，类、方法、变量、参数、包。
3. 注解不会对所修饰的代码产生直接的影响。

## 内置注解

java.lang 中五个：

> @Override：检查该方法是否是重写方法。如果父类或者引用中没有，则编译错误。
>
> @Deprecated：编辑过时方法。编译警告。
>
> @SuppressWarnings：指示编译器忽略注解中声明的警告。
>
> @SafeVarargs：java7 开始支持，忽略任何参数为泛型变量的方法或者构造函数调用产生的警告。
>
> @FunctionalInterface：Java 8 开始支持，标识一个匿名函数或函数式接口。

## 元注解

元注解，即作用于其他注解的注解。在 java.lang.annotation 中，共五个：

> @Retention： 标识这个注解怎么保存，是只在代码中，还是编入class文件中，或者是在运行时可以通过反射访问。
>
> @Documented：标记这些注解是否包含在用户文档中。
>
> @Target：标记这个注解应该是哪种 Java 成员。
>
> @Inherited：标记这个注解是继承于哪个注解类(默认 注解并没有继承于任何子类)。
>
> @Repeatable：允许在相同的程序元素中重复注解。
>
> @Native：修饰成员变量，表示这个变量可以被本地代码引用，常常被代码生成工具使用。对于 @Native 注解不常使用。

每个注解都包含一个 Retention 注解，以及一个或多个 Target 注解。

## 注解三个重要类

```java
package java.lang.annotation;
public interface Annotation {

    boolean equals(Object obj);

    int hashCode();

    String toString();

    Class<? extends Annotation> annotationType();
}
```

```java
package java.lang.annotation;

public enum ElementType {
    TYPE,               /* 类、接口（包括注释类型）或枚举声明  */

    FIELD,              /* 字段声明（包括枚举常量）  */

    METHOD,             /* 方法声明  */

    PARAMETER,          /* 参数声明  */

    CONSTRUCTOR,        /* 构造方法声明  */

    LOCAL_VARIABLE,     /* 局部变量声明  */

    ANNOTATION_TYPE,    /* 注释类型声明  */

    PACKAGE,             /* 包声明  */
        
    TYPE_PARAMETER,		/**参数类型声明*/
    
    TYPE_USE			/**标注任意类型声明*/
}
```

```java
package java.lang.annotation;
public enum RetentionPolicy {
    SOURCE,            /* Annotation信息仅存在于编译器处理期间，编译器处理完之后就没有该Annotation信息了  */

    CLASS,             /* 编译器将Annotation存储于类对应的.class文件中。默认行为  */

    RUNTIME            /* 编译器将Annotation存储于class文件中，并且可由JVM读入 */
}
```

## 自定义注解

e.g.

```java
@Target(ElementType.TYPE)//只能应用于类上
@Retention(RetentionPolicy.RUNTIME)//保存到运行时
public @interface MyAnno {
    String value() default "";//default 用于提供默认值
}

public class MainClass {
    @MyAnno("thisAnno")
    public void test(){
        
    }
}
```

### 自定义注解使用场景

1. 类属性自动赋值。
2. 验证对象属性完整性。
3. 代替配置文件功能，像spring基于注解的配置。
4. 可以生成文档，像java代码注释中的@see,@param等。

### 注意事项

1. 注解支持的元素数据类型包括

   >String
   >
   >所有基本类型（int,float,boolean,byte,double,char,long,short）
   >
   >Class
   >
   >enum
   >
   >Annotation
   >
   >上述类型的数组

2. 元素必须要么具有默认值，要么在使用注解时提供元素的值，元素不能为空

3. 反编译可发现注解实际上是继承了 Annotation 接口，所以自定义注解时，注解不能继承。

## 注解与反射 -- 解析注解

如果我们要获得的注解是配置在方法上的，那么我们要从Method对象上获取；如果是配置在属性上，就需要从该属性对应的Field对象上去获取，如果是配置在类型上，需要从Class对象上去获取。

`isAnnotationPresent(Class<? extends Annotation> annotationClass)`方法是专门判断该元素上是否配置有某个指定的注解；

`getAnnotation(Class<A> annotationClass)`方法是获取该元素上指定的注解。之后再调用该注解的注解类型元素方法就可以获得配置时的值数据；

`getAnnotations()`，该方法可以获得该对象身上配置的所有的注解，包含该对象继承来的注解。它会返回给我们一个注解数组，需要注意的是该数组的类型是Annotation类型，这个Annotation是一个来自于java.lang.annotation包的接口。

`getDeclaredAnnotations()`获取该元素上的所有注解，但不包含该元素继承的注解。

`getParameterAnnotations()`返回类型声明的注解。