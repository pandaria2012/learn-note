* 日期

```
API

** java.util.GregorianCalendar 1.1 **
* GregorianCalendar()
    构造一个日历对象，用来表示默认地区、默认时区的当前时间。
* GregorianCalandar(int year, int month, int day)
* GregorianCalandar(int year,int month, int day, int hour, int minutes, int seconds)
    用给定的日期和时间构造一个Gregorian日历对象。
    year: 该日期所在的年份
    month: 该日期所在的月份，以0为基准;例如，0表示一月
    day: 该月份中的日期
    hour: 小时(0~23)
    minutes: 分钟(0~59)
    seconds: 秒(0~59)
* int get(int field)
    返回给定域的值。
    field: 下述之一: Calendar.ERA、Calendar.YEAR、Calendar.MONTH、
    Calendar.WEEK_OF_YEAR、Calendar.WEEK_OF_MONTH、Calendar.DAY_OF_MONTH、Calendar.DAY_OF_YEAR、Calendar.DAY_OF_WEEK、Calendar.DAY_OF_WEEK_IN_MONTH、Calendar.AM_PM、Calendar.HOUR、Calendar.HOUR_OF_DAY、Calendar.MINUTE、Calendar.SECOND、Calendar.MILLISECOND、Calendar.ZONE_OFFSET、Calendar.DST_OFFSET
* void set(int field, int value)
    设置特定域的值
    field: get接收的常量之一
    value: 新值
* void set(int year, int month, int day)
* void set(int year, int month, int day, int hour, int minutes, int seconds)
    将日期域和时间域设置为新值。
    year: 该日期所在的年份
    month: 该日期所在的月份，以0为基准;例如，0表示一月
    day: 该月份中的日期
    hour: 小时(0~23)
    minutes: 分钟(0~59)
    seconds: 秒(0~59)
* void add(int field, int amount)
    这是一个可以对日期信息实施算数运算的方法。
    对给定的时间域增加指定数量的时间。
    ex: c.add(Calendar.DAY_OF_MONTH, 7),将当前的日历日期加上7
    field: 需要修改的域(get方法参数的某个常量)
    amount: 域被改变的的数量(可以为负值)
* int getFirstDayOfWeek()
    获得当前用户所在地区，一个星期中的第几天。
    ex: 在美国一个星期中的第一天是Calendar.SUNDAY。
* void setTime(Date time)
    将日历设置为指定的时间点
    time: 时间点
* Date getTime()
    获得这个日历对象当前值所表达的时间点。

** java.text.DateFormatSymbols 1.1 **
* String[] getShortWeekdays()
* String[] getShortMonths()
* String[] getWeekdays()
* String[] getMonths()
    获取当前地区的星期几或月份名称。利用Calendar的星期和月份常量作为数组索引值。
```

* final 修饰的类对象属性

```
    可以将实例属性定义final。构建对象时必须初始化这样的属性值。也就是
    说在一个构造器执行后，这个属性值必须被设置，并且在后续的操作中，
    不能在对其进行修改。
    final修饰符大都应用于基本数据类型，或不可变类的域中每个方法都
    不会改变其对象，这种类就是不可变类。ex: String类
    注意: 
        private final Date birthday;
        birthday变量中的对象的引用在对象构造之后不可变，并不代表
        birthday对象是一个常量，birthday引用对象调用setTime来更改。
```
* 静态域(静态属性, 静态变量)

```
    属于类，而不属于任何独立的对象
```
* 静态常量

```
    静态常量使用的比较多
    // Math.PI
    public static final double PI = 3.14159265358979323846;
    // System.out
    public static final PrintStream out = ...;
    虽然都是 public ，但是都被 final 修饰了，所以是没有问题的。
    不允许在被修改。
    System.out = new PrintStream(...);// ERROR--out is final
    // 这里 System 类有一个setOut方法，可以修改System.out。
    // 因为setOut方法是一个本地方法，不是用java语言实现的，
    // 可以绕过Java语言的存取控制机制，这是一种特殊的方法。
```

* 静态方法

```
* 静态方法是一种不能向对象实施操作的方法，换句话说，就是没有隐式参数。
* 静态方法是没有 this 参数的方法。
* 静态方法不能在静态方法中访问实例域。但是可以访问自身类中的静态域。(属于类，不属于类的对象)
* 类可以调用静态方法，对象也可以调用静态方法。但是建议使用类名调用。
    A a = new A();
    a.staticMethod();
    A.staticMethod();
* 何时使用静态方法:
    1. 一个方法不需要访问对象状态，其所需参数都是通过显试参数提供。
    2. 一个方法只需要访问类的静态域。
* 工厂方法:
    返回不同的类的对象
* main 方法:
    main 方法不对任何对象进行操作。在启动程序时还没有任何一个对象。
    静态的main方法将执行并创建程序所需要的对象。
    每个类都可以有一个静态main方法。(入口方法只会是其中一个， java SomeObject)
```

* 方法参数

```
* call by value
* call by reference
* call by name (Algol程序设计语言，现在已经成为历史)

* 方法参数共有两种类型:
    1. 基本数据类型(数字、布尔值)。
    2. 对象引用。
* 方法参数的使用情况:
    1. 一个方法不能修改一个基本数据类型的参数(即数值型和布尔型)。
    2. 一个方法可以改变一个对象参数的状态。
    3. 一个方法不能让对象参数引用一个新的对象。
```

* 对象构造

```
* 重载
    如果有多个方法有相同的名字、不同的参数，便产生了方法重载。
    编译器在挑选匹配那个方法合适的过程叫做重载解析，找不到会产生编译时错误。
    tips:
        Java 允许任何方法重载，方法名和参数类型，叫做方法签名。返回类型不是方法签名的一部分。
        不能有两个名字相同、参数类型也相同却返回不同类型值得方法。
* 默认域的初始化(类的属性初始化默认属性值)
    如果没有显示的给域(属性)赋初值，
```

* tips

```
* 1. 一个文件中，只能有一个公有类，但是可以有任意数目的非公有类。
* 2. 类方法中的局部变量不要与类本身的属性命名相同。
* 3. 每个类方法都有一个隐式参数(第一个参数)
    someObject.someMethod(p);
    someMethod方法有一个隐式参数就是 . 前面的 someObject,不出现在方法名后的 () 中。
    p 是一个显试参数。出现在方法名后的 () 中。
    方法体中 使用 this 来表示隐式参数。
* 4. java的方法都定义在类的内部，但是不是所有的方法都是内联方法。
    是否将某个方法设置为内联方法是jvm的事情，即时编译器会监视调用那些
    简介、经常被调用、没有被重载、以及可优化的方法。
* 5. 类的某个属性是一个对象时(或者是一个引用,可变数据域)。在其get方法是要注意。
    返回该属性的clone对象。而非对对象的引用。
    return someObject.clone();
* 6. ** 一个方法可以访问所有类的所有对象的私有数据 **
    class Employee
    {
        ...
        public boolean equals(Employee other)
        {
            return this.name.equals(other.name);
        }
    }
    ...
    if(someone.equals(boss))...
    // 既访问了someone 的私有域，同时也访问了boss的私有域
    // Employee类的方法可以访问Employee类的任何一个对象的私有域。

```
