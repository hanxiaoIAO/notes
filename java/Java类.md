## 通用

### Math

#### 进位

1. Math.ceil(): 天花板的意思，就是逢余进一
2. Math.floor() : 地板的意思，就是逢余舍一
3. Math.rint(): 四舍五入，返回double值。注意.5的时候会取偶数
4. Math.round(): 四舍五入，float时返回int值，double时返回long值

#### 算术计算

1. `Math.sqrt()` : 计算平方根
2. `Math.cbrt()` : 计算立方根
3. `Math.pow(a, b)` : 计算a的b次方
4. `Math.max( , )` : 计算最大值
5. `Math.min( , )` : 计算最小值
6. `Math.abs()` : 取绝对值

#### 指数函数

1. public static double exp ( double x )  ： e^x
2. public static double log ( double x )  ：  ln x 
3. public static double log10 (double x ) ：  log10 (x) 
4. public static double pow ( double a, double b )： 返回x的y次幂
5. public static double sqrt ( double x ) ： √(x) x的二次方根 

#### 随机数

1. `Math.random()`: random() 方法用于返回一个随机数，随机数范围为 0.0 =< Math.random < 1.0。

## java 8+

### Optional

Optional 存放一个值的容器，该值可能为 null 值。个人认为该类的意义在于明确的表明该容器存放的变量可能为 null。一般用来作为接口的返回值，用来提示调用者处理 NullPointerException。