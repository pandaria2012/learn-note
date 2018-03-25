* array-basic

```
// 声明一个数组
int[] a;
// 声明并赋值
int[] a = new int[100];// 可以存储100个int的数组

// another 声明并赋值
int[] a = { 2, 3, 5, 7, 11, 13 };// 不许要new。
// 初始化一个匿名数组
new int[] { 17, 19, 23, 29, 31, 37 }

// 不创建变量的情况下初始化一个数组
a = new int[] { 17, 19, 23, 29, 31, 37 }
// 等于与下列方法
int[] anonymous = { 17, 19, 23, 29, 31, 37 };
a = anonymous;
```

* 数组拷贝

```
// 引用传递
// 数组变量赋值给另一个数组变量时，两个变量引用的是同一个数组；
int[] a = { 2, 3, 5, 7, 11, 13 };
int[] b = a;
b[5] = 12; // 此时 a[5]=12

// 值传递
// Arrays.copyTo方法
int[] b = Arrays.copyOf(a,a.length * 2);
// 第一个参数是要拷贝的数组, 第二个参数是新数组的长度。
// 第二个参数少于被拷贝数组的长度时，截取; 
// 大于时 按照初始化默认值填充
```

* 数组排序

```
* 数值类型排序，Arrays类的sort方法
    int[] a = new int[1000];
    ...
    Arrays.sort(a);// 快速排序
```

* tips

```
* 初始值
    创建一个数字数组时，所有元素都初始化为0。boolean数组的元素初始化为false。对象数组的元素初始化为null。
* 数组长度
    array.length 属性获得元素个数
    访问数组时，注意数组越界问题，会异常而终止。
    ** java中允许数组长度为0，注意0与null不同 **
* 长度在初始化时固定
    一旦创建了数组，就不能再改变它的大小（每个元素是可以改变的）。
    运行过程中需要改变扩展数组的大小，可以使用数组列表(array list)
* 打印数组的值
    可以使用 Arrays.toString(a)返回一个包含数组元素的字符串。
* 与c++相比，java中的 [] 运算符被定义为检查数组边界;并没有指针运算
* 命令行参数
    java Test -a hello world
    args[0]为 "-a"
    args[1]为 "hello"
    args[2]为 "world"
```

* API

```
* static String toString(type[] a) 5.0
    返回包含a中数据元素的字符串，这些元素放在括号内，并用逗号分隔。
    a: 类型为 int,long,short,char,byte,
        boolean,float,double的数组。
* static type copyOf(type[] a, int length) 6
* static type copyOf(type[] a, int start, int end) 6
    返回与a类型相同的一个数组，其长度为length或end-start。
    a: 类型为 int,long,short,char,byte,
        boolean,float,double的数组。
    start: 起始下标(包含这个值)。
    end: 终止下标(不包含这个值)。
        大于a.length的额外的为相应的默认值。
    length: 拷贝的数据元素的长度，与end解释相同
* static void sort(type[] a)
    采用优化的快速排序算法对数组进行排序。
    a: 类型为 int,long,short,char,byte,
        boolean,float,double的数组。
* static int binarySearch(type[] a, type v)
* static int binarySearch(type[] a, int start, int end, type v) 5
    采用二分搜索算法查找v。查找成功，返回对应的下标;
    否则返回一个负数值r。-r-1 是为保持a有序v应插入的位置。
    a: 类型为 int,long,short,char,byte,
        boolean,float,double的有序数组。
    start: 起始下标(包含这个值)。
    end: 终止下标(不包含这个值)。
    v: 同a的数据元素类型相同的值。
* static void fill(type[] a, type v)
    将数组的所有数据元素值设置为v
    a: 类型为 int,long,short,char,byte,
        boolean,float,double的有序数组。
    v: 与a数据元素类型相同的一个值。
* static boolean equals(type[] a, type[] b)
    如果两个数组大小相同，并且下标相同的元素都相应相等，返回ture。
    a,b: 类型为 int,long,short,char,byte,
        boolean,float,double的两个数组。

```