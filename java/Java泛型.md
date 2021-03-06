## 泛型概念

泛型是Java SE 1.5的新特性，泛型的本质是参数化类型。

泛型可以用在类、接口和方法的创建中，分别称为泛型类、泛型接口、泛型方法。

在Java SE 1.5之前，没有泛型的情况的下，通过对类型Object的引用来实现参数的“任意化”，“任意化”带来的缺点是要做显式的强制类型转换，而这种转换是要求开发者对实际参数类型可以预知的情况下进行的。对于强制类型转换错误的情况，编译器可能不提示错误，在运行的时候才出现异常，这是一个安全隐患。泛型的好处是在编译的时候检查类型安全，并且所有的强制转换都是自动和隐式的，以提高代码的重用率。

## 泛型通配符？，T，E，K，V区别

功能相同，只是名称上一个约定的习惯，通常：

> - **？** 表示不确定的java类型
> - **T (type)** 表示具体的一个java类型
> - **K V (key value)** 分别代表java键值中的Key Value
> - **E (element)** 代表Element

