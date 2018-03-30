### 对象包装器与自动装箱
    所有的基本类型都有一个与之对应的类。ex: int对应Integer类。这些类成为包装器。包括:
    Integer、Long、Float、Double、Short、Byte、Character、Void和Boolean(前6个属于Number类的子类)。

1. 包装器类是不可变的，一旦创建了，就不允许修改包装在其中的值。
2. 对象包装器类还是final，所以也不能被继承。

tips: Integer的效率肯定是没有int好。

* 自动装箱拆箱:

```java
ArrayList<Integer> list = new ArrayList<>();
list.add(3); 
// 自动转变为下面的方式
list.add(Integer.valueOf(3));
//这种变换方式称之为 自动装箱

// 相反的，也有自动拆箱
int n = list.get(i);
// 会自动转成下面的方式
int n = list.get(i).intValue();

// 自动装箱拆箱
Integer n = 3;
n++; // 拆箱 ---> 进行自增计算 ---> 在将结果装箱
```

* tips:

    自动装箱规范的要求，boolean、byte、char<= 127，在 -128 ~ 127 之间的 short 和
    int 被包装到固定的对象中。

    ** 装箱和拆箱是编译器的行为，虚拟机并不参与 **

    ** Integer对象是不可变的: 包含在包装器中的内容是不会改变的 **

    org.omg.CORBA包中有持有者类型，ex: IntHolder、BooleanHolder等，可以改变其中的值。

* API: java.lang.Integer 1.0
    
    * int intValue()
        
        以 int 的形式返回 Integer 对象的值(在Number类中覆盖了intValue类);

    * static String toString(int i)

        以一个新String对象的形式返回给定数值i的十进制表示。

    * static String toString(int i, int radix)
    
        返回数值i的基于给定radix参数进制的表示。

    * static int parseInt(String s)
    * static int parseInt(String s, int radix)

        返回字符串s表示的整型数值，给定字符串表示的是十进制的整数(第一种方法),
        或者是radix参数进制的整数(第二种方法)。

    * static Integer valueOf(String s)
    * static Integer valueOf(String s, int radix)

        返回用s表示的整型数值进行初始化后的一个新Integer对象，给定字符串表示的是
        十进制的整数(第一种方法)，或者是radix参数进制的整数(第二种方法)。

* API: java.text.NumberFormat 1.1 

    * Number parse(String s)

        返回数字值，假设给定的String表示了一个数值。
