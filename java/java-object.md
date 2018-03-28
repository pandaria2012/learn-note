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
    如果没有显示的给域(属性)赋初值，那么他们就会被显示的赋默认值: 
    数值为0、布尔值为false、对象引用为null。
    注意，null，所以一般都要显示的赋值，避免空指针问题。
* 无参数的构造器
    仅当类没有提供任何构造器的时候，系统才会提供一个默认的构造器。
* 显示域初始化
    在执行构造器之前，先执行赋值操作。
    ex:
        class Employee
        {
            private String name = "";
            ...
        }
        class Employee
        {
            private static int nextId;
            private int id = assignId();
            ...
            private static int assignId()
            {
                int r = nextId;
                nextId++;
                return r;
            }
            ...
        }
* 调用另一个构造器
    this 关键字，另一个含义。
    public Employee(double s)
    {
        this("Employee #" + nextId, s);
        nextId++;
    }
    当 new Employee(60000)时，Employee(double)构造器将调用Employee(String, double)构造器。
* 初始化块
    初始化数据域的方式:
        1. 在构造器中设置值。
        2. 在声明中赋值。
    3. 初始化块。
    一个类的声明中，可以包含多个代码块。只要构造类的对象，这些代码块就会被执行。
    ex:
        class Employee
        {
            private static int nextId;

            private int id;
            private String name;
            private double salary;

            // 对象初始化块
            {
                id = nextId;
                nextId++;
            }

            public Employee(String n, double s)
            {
                name = n;
                salary = s;
            }

            public Employee()
            {
                name = "";
                salary = 0;
            }
            ...
        }
    先执行初始化块，在执行构造器。
    ** 建议在初始化块放在域定义之后，两者挨着 **

    ** 调用构造器的具体处理步骤 **
    1. 所有数据域被初始化为默认值(0,false或null)。
    2. 按照在类声明中出现的次序，依次执行所有域初始化语句和初始化块。
    3. 如果构造器第一行调用了第二个构造器，则执行第二个构造器主体。
    4. 执行这个构造器的主体。

    对于静态数据域的初始化，如果非常复杂，可以使用静态的初始化块。
    ex:
        // 静态初始化块
        static
        {
            Random generator = new Random();
            nextId = generator.nextInt(10000);
        }
        // 在类第一次加载的时候，将会执行此部分代码。
    tips:
        编写一个没有main方法的“Hello World”程序。
        public class Hello
        {
            static
            {
                System.out.println("Hello World!");
            }
        }
```

* 对象析构与finalize方法

```
相比较c++，Java有自动的垃圾回收器，不需要人工回收，所以java不支持析构器(析构方法)。
但是当某些对象使用了内存之外的其他资源，如文件使用了系统资源的另一个对象的句柄。当资源
不在需要时，将其回收和在利用就很有必要了。

可以为任何一个类添加 finalize 方法。fianlize 方法将在垃圾回收器清除对象之前调用。
但是在实际开发中，不要依赖 finalize 方法回收任何短缺的资源，因为此方法何时被调用很难确定。

如果某个资源需要在使用完毕后立刻被关闭，那么就需要人工来管理。对象用完时，
可以用一个close方法来完成相应的清理工作。
```

* 包

```
* 包的主要作用是确保类名的唯一性。
* 类的导入
    一个类可以使用所属包中的所有类，以及其他包中的公有类(public class)。
    import 语句导入一个特定的类或者整个包，import 语句应在文件顶部，package语句后面。
    类名冲突怎么办？
        import java.util.*;
        import java.sql.*;
        两个包中都有Data类。会出现编译错误。
        1. 增加一个特定的import语句来解决。
            import java.util.*;
            import java.sql.*;
            import java.util.Date;
        2.如果两个Date类都使用怎么办？
            // 在使用时，加上完整包名。
            java.util.Date deadline = new java.util.Date();
            java.sql.Date today = new java.sql.Date(...);
* 静态导入
    import 语句还可以导入静态方法和静态域的功能。
    ex:
        import static java.lang.System.*;
        // 此时就可以使用System类的静态方法和静态域了
        out.println("Goodbye!");// System.out
        exit(0);// System.exit

        // 也可以只导入特定的方法或域
        import static java.lang.System.out;
* 将类放入包中
    将包名放在源文件的开头，包中定义的类的代码之前，就可以了。
    如果没有在源文件中写package语句，这个源文件中的类将被放置到
    一个默认包(default package)中。默认包是一个没有名字的包。差不多是项目根目录。

    java com/company/App.java
    javac com.company.App
    编译器对文件进行操作(com/company/App.java)。
    java解释器加载类(javac com.company.App)。

    tips:
        编译器在编译源文件时不会检查目录结构。如果源文件没有在其包名所对应的相应目录下，
        也可以进行编译。并且如果它不依赖于其他包，就不会出现编译错误。但是程序仍旧无法运行

* 包作用域
    public 修饰的可以被任意类使用; private 修饰的只能被定义他们的类使用。
    如果没有public或private修饰，可以被同一个包中的所有方法访问。

    ** 包密封(package sealing)机制 ** 解决将各种包混杂在一起的问题。
```

* 类路径

```
* 类的路径名必须与包名匹配
* jar包

* 使类能够被多个程序共享。
    1. 把类放到一个目录中。
    2. 将jar文件放在一个目录中。
    3. 设置类路径(class path)。类路径是所有包含类文件的路径的集合。
    运行时库文件(rt.jar和在jre/lib与jre/lib/ext目录下的一些其他jar文件)会被自动搜索。
    所以他们不必显试的列在类路径中。

    * 虚拟机找类文件时
        1. 首先查看 jre/lib 和 jre/lib/ext目录下的归档文件中所存放的所有的系统类文件。
        2. 然后再去类路径(class path)的路径中找相应的类文件。
    * 编译器定位文件: 如果引入了一个类，而没有指定这个类所在的包。
        1. 首先查找包含这个类的包，并查询所有import指令，确定其中是否包含了被引用的类。
        2. 基于第一步，查找这些包和当前包，对其中的每个类进行逐一查看。
        3. 如果找到了一个以上的类，就会产生编译错误(因为类必须是唯一的，
            和import语句的顺序无关)。
        4. 如果找到了唯一的一个这个类，查看其源文件是否比类文件新。
            如果新，重新编译此类。
    tips:
        公有类: 一个源文件只能包含一个公有类，且文件名必须与公有类匹配。所以，编译器很容易
        定位共有类所在的源文件。
        非共有类: 如果从当前包中导入非共有类。这些类有可能定义在于类名不同的源文件中。
        那么编译器就会搜索当钱包中的所有源文件，以便确定那个源文件定义了这个类。
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

* 类的设计技巧
    1. 一定要保证数据私有。
    2. 一定要对数据初始化。
    3. 不要在类中使用过多的基本类型。
        比如，用户类(User)中的地址字段换成地址类(Address),而Address包含以下属性
        private String street;
        private String city;
        private String state;
        private int zip;
        这样可以很容易处理地址的变化。
    4. 不是所有的域都需要独立的域访问器和域更改器。
        比如，雇员对象中的雇佣日期，就不应该被修改。
    5. 将职责过多的类进行分解。
    6. 类名和方法名要能够体现他们的职责。

```
