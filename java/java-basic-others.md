* 大数值

```
BigInteger 和 BigDecimal (java.math)
    * BigInteger 实现了任意精度的整数运算。
    * BigDecimal 实现了任意精度的浮点数运算。
    
// 使用静态方法 valueOf 方法将普通的数值转换成大数值
BigInteger a = BigInteger.valueOf(100);
// 不能使用 + * 方法需要用 add muitiply 方法
BigInteger c = a.add(b);
BigInteger d = c.multiply(b.add(BigInteger.valueOf(2)));

// java 中没有 c++ 中的运算符重载功能

* API 
* java.math.BigInteger 1.1
* BigInteger add(BigInteger other)
    和
* BigInteger subtract(BigInteger other)
    差
* BigInteger multiply(BigInteger other)
    积
* BigInteger divide(BigInteger other)
    商
* BigInteger mod(BigInteger other)
    返回这个大整数和另一个大整数的余数
* int compareTo(BigInteger other)
    如果这个大整数与另一个大整数other相等，返回0，大于返回正数，
    小于返回负数
* static BigInteger valueOf(BigInteger x)
    返回等于x的大整数

* java.math.BigDecimal 1.1
* BigDecimal add(BigDecimal other)
    和
* BigDecimal subtract(BigDecimal other)
    差
* BigDecimal multiply(BigDecimal other)
    积
* BigDecimal divide(BigDecimal other, RoundingMode mode) 5.0
    商, 必须给出舍入方式 ex: RoundingMode.HALF_UP(四舍五入)
* BigDecimal compareTo(BigDecimal other)
    相等，返回0; 大于, 返回正数; 小于，返回负数;
* BigDecimal valueOf(long x)
* BigDecimal valueOf(long x, int scale)
    返回 x 或 x/10^scale 的一个大实数
```