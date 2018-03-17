### java的基本数据类型
    
    
    
    * 整型
        * int 4字节 -2147483648 ~ 2147483647 （-2^(4*8-1) ~ 2^(4*8-1)-1）
        * short 2字节 -32768 ~ 32767 （-2^(2*8-1) ~ 2^(2*8-1)-1）
        * long 8字节 -9223372036854775808 ~ 9223372036854775807 （-2^(8*8-1) ~ 2^(8*8-1)-1）
        * byte 1字节 -128 ~ 127（-2^7 ~ 2^7-1）
        
    * 浮点类型
        * float 4字节 有效位数为6~7位
        * double 8字节 有效位数为15位
        
        tips:
            正无穷大 (Double.POSITIVE_INFINITY, Float.POSITIVE_INFINITY)
            负无穷大 (Double.NEGATIVE_INFINITY, Float.NEGATIVE_INFINITY)
            NaN (Double.NaN, Float.NaN)
            一个正整数除以0为正无穷大，而 0/0 或者负数的平方根为 NaN；
            
    * char类型
        * 用来表示单个字符。通常用来表示字符常量。
            * 'A'和"A"表示的含义是不一样的，'A' 是编码为65所对应的字符常量，"A" 是一个包含A的字符串
        * 在java中，char类型用UTF-16编码描述一个代码单元。
    
    * boolean 类型
        * true
        * false
        
        tips:
            整型值和布尔值之间不能进行互相转换；
        
        


### 变量
    
    * 每一种变量都属于一种类型
    * 'A'~'Z','a'~'z','_','$'或在某种语言中代表字母的任何Unicode字符.
        * Character类的 isJavaIdentifierStart 和 isJavaIdetifierPart 方法检测哪些Unicode字符属于java中的"字母"
        * $ 虽然合法,但是尽量不要在自己的代码中使用这个字符,它只在java编译器或其他工具生成的名字中.
    * 最好将变量的声明和赋值放在一起(初始化, 默认值)
    
    
### 常量
    
    * final 关键字指示常量(final表示这个变量只能被赋值一次,一旦赋值就不能在更改了).
    
        ```
        public static void main(String[] args)
        {
            final double PI = 3.14;
        }
        ```
        
    * 类常量 static final 来设置一个类常量.
    
        ```
        public class Constants
        {
            public static final double PI = 3.14;
            public static void main(String[] args)
            {
                System.out.println("PI="PI);
            }
        }
        ```
        
        
        
### 运算符

    * 当参与 / 运算的两个操作数都为整数时,表示整数除法;否则表示浮点除法.
    ```
    15/2=7
    15.0/2=7.5
    ```
    * 取模 15%2=1
    * ** 整数被0除会产生异常,浮点数被0除会得到无穷大或NaN **
    
    tips:
        strictfp 关键字标记的方法必须使用严格的浮点计算来产生理想的结果
        ```
        public static strictfp void main(String[] args)
        // 在 main 方法中的所有指令都将使用严格的浮点计算,
        // 如果将一个类标记为 strictfp, 这个类中的所有方法都要使用严格的浮点计算
        ```

    * \>\>\> 运算符将用0填充高位; >> 运算符用符号位填充高位,没有 <<< 运算符.
        ```
        对于移位运算符右侧的参数需要进行模32的运算(如果左边的操作数是long类型,那么会进行模64运算).也就是说
        1 << 35 和 1 << 3 或 8 是相同的
        ```


### 数学函数与常量
    
    * Math 类
        ```
        Math.sin
        Math.cos
        ...
        Math.exp
        Math.log
        ```
    * 数学常量
        ```
        Math.PI
        Math.E
        ```
    tips:
        * 静态导入
        ```
        import static java.lang.Math.*;
        ...
        System.out.println("The square root of \u03c0 is " + sqrt(PI));
        ```
        * StrictMath 类
        ```
        Math 类的性能比较快, 所有的方法都使用计算机浮点单元中的例程.
        StrictMath 类 可以保证在所有平台上得到相同的计算结果,但是运行速度比 Math 类慢.
        ```
        
### 数值类型之间的转换

** 数值类型之间的合法转换 **
![](/assets/java数值类型之间的合法转换.png)

```
实心箭头表示,无信息丢失的转换, 虚箭头表示,可能有精度损失的转换
```

两个数值进行二元操作时, 都会将两个操作数转换为同一种类型, 然后在进行计算.规律就是 像精度高的类型转换, 有一个是 double ,另一个就会转 double, 否则, 两个都将被转 int .

### 强制类型转换
    
    ```
    double x = 9.997;
    int nx = (int) x; // nx 的值为 9; 截断小数部分
    // ----------
    double x = 9.997;
    int nx = (int) Math.round(x); // nx = 10; round 的返回结果为long, 还是需要强转一下为int;
    ```
** 注意, 高精度像低精度强转时, 因为溢出造成的问题 **

### 运算符优先级
![](/assets/java运算符优先级.png)






