** java字符串就是Unicode字符序列. 字符串不是一种类型, 而是一个预定义类, String类. **

* 子串
```
String greeting = "Hello";
String s = greeting.substring(0,3); // s = "Hel"
```

* 拼接
```
** + ** 连接两个字符串
任何一个java对象都可以转换成字符串
```

* 不可变字符串
```
1.String类对象称为不可变字符串
2.字符串常量
3.编译器可以让字符串共享
```

* 检测字符串是否相等
```
s.equals(t)
s.equalsIgnoreCase(t)
s.compareTo(t) == 0 // 也可以
** 注意一定不能使用 == **
== 只能确定 两个字符串是否放置在同一个位置上.
```

* 空串与null串
```
空串是一个java对象,串长度为0,内容为空
检查字符串是否为空
str.length() == 0
str.equals("")
检查一个字符串是否为null
str == null
str != null && str.length() != 0 // 检查一个字符串既不是null也不为空串
```

* 代码点(字节)与代码单元(字符)

```
String greeting = "Hello";
int n = greeting.length(); // n代码单元数量(字符数)
int cpCount = greeting.codePointCount(0,greeting.length()); // cpCount 代码点数量(字节数)
调用s.charAt(n)返回位置n的代码单元, 0 < n < s.length()-1
char first = greeting.charAt(0); // first = 'H'
第I个代码点(字节), 如下:
int index = greeting.offsetByCodePoints(0, i);
int cp = greeting.codePointAt(index); 

// public int offsetByCodePoints(int index, int codePointOffset)
//  返回此字符串的索引. index 为要偏移的索引(代码点其实位置), 代码点中的偏移量

遍历一个java字符串
    正向遍历
    int cpCount = s.codePointCount(0, s.length());
    for (int i = 0; i < cpCount; i++) {
        int index = s.offsetByCodePoints(0, i);
        int cp = s.codePointAt(index);
        // java.lang.Character.isSupplementaryCodePoint(int codePoint) 确定指定字符(Unicode代码点)是否在补充字符范围。
        if (!Character.isSupplementaryCodePoint(cp)) {
            System.out.println((char) cp);
        } else {
            System.out.println(cp);
            i++;
        }
    }
    反向遍历
    for (int i = s.length() -1; i >= 0 ; i--) {
        int cp = 0;
        if (i == 0) {
            cp = s.codePointAt(0);
            System.out.println((char) cp);
        } else {
            i--;
            cp = s.codePointAt(i);
            if (Character.isSupplementaryCodePoint(cp)) {
                System.out.println(cp);
            } else {
                i++;
                cp = s.codePointAt(i);
                System.out.println((Char)cp);
            }
        }
    }
```


* 字符串API





