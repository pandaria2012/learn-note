* tips：

```
    没有goto语句，但是break可以带标签
```

* 块作用域

```
public static void main(String[] args)
{
    int n;
    ...
    {
        int k;
    } // k只在此块作用于内可用
    
    {
        int k;
        int n;// 编译错误
    }
}
```

* if
 
```
if (condition) statement1 else statement2;
// 多条执行语句的话
if (condition) 
{
    statement1;
    statement2;
} 
else
{
    statement3;
    statement4;
} 
```

* 循环(do{}while();while(){};for(;;){};)

break;
continue;
label:(跳转点声明)

增强for循环
for(variable : collection) statement
collection 必须是一个数组或一个实现Iterable接口的类对象(如ArrayList)。
其他略。。。

