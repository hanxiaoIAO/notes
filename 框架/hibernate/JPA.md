## JPA

JPA是Java Persistence API的简称，中文名Java持久层API，是JDK 5.0注解或XML描述对象－关系表的映射关系，并将运行期的实体对象持久化到数据库中。

JPA的总体思想和现有Hibernate等ORM框架大体一致。总的来说，JPA包括以下3方面的技术：

- ORM映射元数据
  JPA支持XML和JDK5.0注解两种元数据的形式，元数据描述对象和表之间的映射关系，框架据此将实体对象持久化到数据库表中；

- API
  用来操作实体对象，执行CRUD操作，框架在后台替代我们完成所有的事情，开发者从繁琐的JDBC和SQL代码中解脱出来。

- 查询语言
  这是持久化操作中很重要的一个方面，通过面向对象而非面向数据库的查询语言查询数据，避免程序的SQL语句紧密耦合。

## 对象关系映射（Object Relational Mapping，简称ORM）

是通过使用描述对象和数据库之间映射的元数据，将面向对象语言程序中的对象自动持久化到关系数据库中。本质上就是将数据从一种形式转换到另外一种形式。 这也同时暗示着额外的执行开销；然而，如果ORM作为一种中间件实现，则会有很多机会做优化，而这些在持久层并不存在。 更重要的是用于控制转换的元数据需要提供和管理；但是同样，这些花费要比维护手写的方案要少；而且就算是遵守ODMG（面对对象的数据库标准 / Object Data Management Group）规范的对象数据库依然需要类级别的元数据。 

是随着面向对象的软件开发方法发展而产生的。面向对象的开发方法是当今企业级应用开发环境中的主流开发方法，关系数据库是企业级应用环境中永久存放数据的主流数据存储系统。对象和关系数据是业务实体的两种表现形式，业务实体在内存中表现为对象，在数据库中表现为关系数据。内存中的对象之间存在关联和继承关系，而在数据库中，关系数据无法直接表达多对多关联和继承关系。因此，对象-关系映射(ORM)系统一般以中间件的形式存在，主要实现程序对象到关系数据库数据的映射。
  常见的ORM框架有：Hibernate

## JPA概览

  ![JPA概念](resources\JPA概念.png)

  ![JPA注解](resources\JPA注解.png)

## 注解

### @GeneratedValue

1. 为一个实体生成一个唯一标识的主键。@GeneratedValue 提供了主键的生成策略。

2. 有两个属性，分别是 strategy 和 generator。

   > generator属性的值是一个字符串,默认为"",其声明了主键生成器的名称  

   > strategy属性提供四种值:  
   >
   > - AUTO主键由程序控制, 是默认选项 ,不设置就是这个  
   >
   > - IDENTITY 主键由数据库生成, 采用数据库自增长, Oracle不支持这种方式  
   >   &emsp; &emsp; 此种主键生成策略就是通常所说的主键自增长,数据库在插入数据时,会自动给主键赋值,比如MYSQL可以在创建表时声明"auto_increment"   来指定主键自增长。该策略在大部分数据库中都提供了支持(指定方法或关键字可能不同),但还是有少数数据库不支持,所以可移植性略差。使用自增长主键生成策略是只需要声明strategy  = GenerationType.IDENTITY即可。类似于
   >
   >   ```java
   >   @Id 
   >   @GeneratedValue(strategy = GenerationType.IDENTITY)  
   >   private Integer id;  
   >   ```
   >
   >    &emsp; &emsp; 需要注意的是,同一张表中自增列最多只能有一列。
   >
   > - SEQUENCE 通过数据库的序列产生主键, MYSQL  不支持  
   >   &emsp; &emsp; 在某些数据库中,不支持主键自增长,比如Oracle,其提供了一种叫做"序列(sequence)"的机制生成主键。此时,GenerationType.SEQUENCE就可以作为主键生成策略。该策略的不足之处正好与TABLE相反,由于只有部分数据库(Oracle,PostgreSQL,DB2)支持序列对象,所以该策略一般不应用于其他数据库。类似的,该策略一般与另外一个注解一起使用@SequenceGenerator,@SequenceGenerator注解指定了生成主键的序列.然后JPA会根据注解内容创建一个序列(或使用一个现有的序列)。如果不指定序列,则会自动生成一个序列SEQ_GEN_SEQUENCE。类似于
   >
   >   ```java
   >   @Id  
   >   @GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "menuSeq")  
   >   @SequenceGenerator(name = "menuSeq", initialValue = 1, allocationSize = 1, sequenceName = "MENU_SEQUENCE")  
   >   private Integer id; 
   >   ```
   >
   >    &emsp; &emsp; 同样,在以上例子中,menuSeq唯一的标识了该生成器,@SequenceGenerator可以理解为将数据库中存在的序列进行了一个映射,在@GeneratedValue注解中的generator属性可以根据此标识来声明主键生成器。
   >
   > - TABLE 提供特定的数据库产生主键, 该方式更有利于数据库的移植  
   >   &emsp;&emsp;  使用一个特定的数据库表格来保存主键,持久化引擎通过关系数据库的一张特定的表格来生成主键,这种策略的好处就是不依赖于外部环境和数据库的具体实现,在不同数据库间可以很容易的进行移植,但由于其不能充分利用数据库的特性,所以不会优先使用。该策略一般与另外一个注解一起使用@TableGenerator,@TableGenerator注解指定了生成主键的表(可以在实体类上指定也可以在主键字段或属性上指定),然后JPA将会根据注解内容自动生成一张表作为序列表(或使用现有的序列表)。如果不指定序列表,则会生成一张默认的序列表,表中的列名也是自动生成,数据库上会生成一张名为sequence的表(SEQ_NAME,SEQ_COUNT)。序列表一般只包含两个字段:第一个字段是该生成策略的名称,第二个字段是该关系表的最大序号,它会随着数据的插入逐渐累加。类似于  
   >
   >   ```java
   >   @Id    
   >   @GeneratedValue(strategy = GenerationType.TABLE, generator = "roleSeq")  
   >   @TableGenerator(name = "roleSeq", allocationSize = 1, table = "seq_table", pkColumnName = "seq_id", valueColumnName = "seq_count")    
   >   private Integer id;   
   >   ```
   >
   >    &emsp; &emsp; 在以上例子中,roleSeq唯一的标识了该生成器,在@GeneratedValue注解中的generator属性可以根据此标识来声明主键生成器。

