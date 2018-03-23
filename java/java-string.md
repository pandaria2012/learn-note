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
    
```
* char charAt(int index)
    返回给定位置的代码单元。
* int codePointAt(int index)
    返回从给定位置开始或结束的代码点。
* int offsetByCodePoints(int startIndex, int cpCount)
    返回从 startIndex 代码点开始，位移cpCount后的代码点索引。
* int compareTo(String other)
    按照字典顺序，如果字符串位于other之前，返回一个负数；如果字符串位于other之后，返回一个正数；如果两个字符串相等，返回0。
* boolean endsWith(String suffix)
    如果字符串以suffix结尾，返回 true。
* boolean startsWith(String prefix)
    如果字符串以prefix字符串开始，返回 true。
* boolean equals(Object other)
    如果字符串与other相等，返回 true。
* boolean equalsIgnoreCase(String other)
    如果字符串与other相等（忽略大小写）,返回true。
* int indexOf(String str)
* int indexOf(String str, int fromIndex)
* int indexOf(int cp)
* int indexOf(int cp, int fromIndex)
    返回与字符串str或代码点cp匹配的第一个子串的开始位置。这个位置
    从索引0或fromIndex开始计算。如果在原始串中不存在str,返回 -1.
* int lastIndexOf(String str)
* int lastIndexOf(String str, int fromIndex)
* int lastIndexOf(int cp)
* int lastIndexOf(int cp, int fromIndex)
    返回与字符串str或代码点cp匹配的最后一个子串的开始位置，
    这个位置从原始串尾端或fromIndex开始计算。
* int length()
    返回字符串的长度。
* int codePointCount(int startIndex, int endIndex)
    返回startIndex 和 endIndex - 1 之间的代码点数量。
    没有匹配成对的代用字符将计入代码点。
* String replace(CharSequence oldString, CharSequence newString)
    返回一个新的字符串。这个字符串用newString代替原始字符串中
    所有的oldString。可以用String或StringBuilder对象
    作为CharSequence参数
* String substring(int beginIndex)
* String substring(int beginIndex, int endIndex)
    返回一个新字符串。这个字符串包含原始字符串中从beginIndex
    到串尾或endIndex-1的所有代码单元
* String toLowerCase()
* String toUpperCase()
    大小写转换
* String trim()
    删除原始字符串头部和尾部的空格。
```

* 构建字符串（ + 方式效率比较低，耗时浪费空间）
```
** StringBuilder 类 **
// 创建构建器
StringBuilder builder = new StringBuilder();
// 添加内容
builder.append(ch); // ch = 'a'
builder.append(str); // str = "bcd"
// 调用toString方法获得String对象
String completedString = builder.toString();
//方法列表
* int length()
    返回构建器或缓冲器中的代码单元数量。
* StringBuilder append(String str)
    追加一个字符串并返回 this。
* StringBuilder append(char c)
    追加一个代码单元并返回this。
* void setChartAt(int i, char c)
    将第i个代码单元设置为c
* StringBuilder insert(int offset, String str)
    在offset位置插入一个字符串并返回this。
* StringBuilder insert(int offset, Char c)
    在offset位置插入一个代码单元并返回this。
* StringBuilder delete(int startIndex, int endIndex)
    删除偏移量从startIndex到endIndex-1的代码单元并返回 this。
* String toString()
    返回一个与构建器或缓冲器内容相同的字符串。
```



