### 参数数量可变的方法

```
System.out.printf("%d %s", 10, "ABc");
// 如此声明main方法
public static void main(String... args)

// 自己声明一个可变参数的方法
public static double max(double... values)
{
    double largest = Double.MIN_VALUE;
    for(double v : values) if(v > largest) largest = v;
    return largest;
}
double m = max(8.7, 3.14, -3.14);
```