### 继承(extend)

##### 多态

```
一个对象变量可以指示多种实际类型的现象叫做多态。
一个A变量既可以引用一个A类对象，也可以引用一个A类的任何一个子类的对象。
当然反过来是不行的，不能将一个超类的引用赋给子类变量。
tips:
    在Java中，子类数组的引用可以转换成超类数组的引用，而不需要采用强制类型转换。
    A[] a = new A[10];
    B[] b = a; // B是A的父类，A extend B;
    b[0] = new B(); // OK 编译器通过。
    // 此时 a[0]和b[0] 引用的是同一个对象。
    // 如果someMethod方法在A类的对象中，父类B没有该方法。
    // 那么 b[0].someMethod()调用时就会发生问题。
    为了防止此类错误的发生，所有数组都要牢记常见他们的元素类型，并负责监督仅
    将类型兼容的引用存储到数组中。
```

##### 动态绑定

```
调用对象方法的执行过程。
    1. 编译器查看对象的声明类型和方法名。
        ex:
            假设调用x.f(p)，且隐式参数x为C类的对象。此时有可能存在多个名字为f,
            但参数类型不同的方法。编译器会获得所有C类中名为f的方法和其超类中访问属性
            为public且名为f的方法(超类的私有方法不可访问)。
        至此，编译器获得所有可能被调用的候选方法。
    2. 接下来，编译器会查看调用方法时提供的参数类型。如果在所有名为f的方法中存在
        一个与提供的参数类型完全匹配，就用此方法。---此过程被称为 重载解析 。
        ex:
            对于x.f("Hello")，编译器会选择f(String)，而不是f(int)。
            由于允许类型转换(int 转 double等)，所以此过程会变的复杂。
            如果编译器没有找到与参数类型匹配的方法，或经过类型转换后，
            得到了多个方法与之匹配，就会报错。
        至此，编译器已获得需要调用的方法名字和参数类型。
        tips:
            子类可以重写父类的方法，但是注意返回类型不是方法签名的一部分，
            所以在重写父类方法时，要注意返回类型的兼容性。
            public Parent getSelf() {...}
            public Child getSelf() {...}
    3. private、static、final方法或者构造器，那么编译器可以准确的知道调用哪个方法，
        这种调用方式称为静态绑定。此时，调用的方法依赖于隐式参数的试剂类型，并且在运行
        时实现动态绑定。
    4. 当程序运行时，并且采用动态绑定调用方法时，虚拟机一定调用与x所引用对象的
        实际类型最合适的那个类的方法。
        虚拟机会预先给每个类创建一个 ** 方法表 ** ，其中会列出所有的方法的签名和
        实际调用的方法。在调用方法时，虚拟机会查询这个表。如果在隐式参数(当前对象的类)
        的类的方法表中找不到相应的方法时，会去搜索其父类的方法表。如果调用了super.f(p),
        编译器将会对饮食参数的父类方法表进行搜索。

    tips:
        在覆盖(override)一个方法时，子类方法不能低于父类方法的可见性。尤其是，父类
        方法为public时，子类方法一定要声明为public。
```

##### 阻止继承: final类和方法

```
如果一个类被final关键字修饰，那他就不能被继承。(final类中的所有方法也自动为final方法)。
类中的特定方法也可以被声明为final，此种方法不能被子类所覆盖。
    tips:
        类中的域(属性)也可以被声明为final。构造对象后就不允许被修改了。
        final类中的方法会自动成为final方法，但是其域(属性)不是。

多态可能在性能上有损耗？
    如果一个方法没有被覆盖并且很短，编译器就能够对他进行优化处理，这个过程称之为内联。
ex: 内联调用e.getName()将被替换为访问e.name域。如果getName方法在另外一个类中被覆盖了，
那么编译器将无法知道覆盖的代码会做什么操作，就不能对其进行内联优化了。
```

##### 强制类型转换
* 只能在继承层次内进行类型转换。
* 在将超类转换成子类之前，应该使用 instanceof 进行检查。

```
    tips:
        x = null;
        x instanceof C // 返回false，并不会产生异常。
```

##### 抽象类
* 包含一个或多个抽象方法的类本身必须被声明为抽象的，抽象类。
* 如果一个类被声明为abstract类，那么就不能创建这个类的对象。
```
abstract class Person
{
    private String name;

    public Person(String n)
    {
        this.name = n;
    }

    public abstract String someAbstractMethod();
}

```

##### 受保护访问
* protected
* tips:

    * Java中的protected部分对所有子类及 **同一个包中的所有其他类** 都可见。
    * 控制可见的四个访问修饰符:
    
        * 对本类可见---private。
        * 对所有类可见---public。
        * 对本包和所有子类可见---protected。
        * 对本包可见---默认，不需要修饰符。


##### tips:

* super 关键字解释:

    super 与 this引用 是两个不同的概念，super不是一个对象的引用，不能将super赋给
    另一个对象变量，它只是一个指示编译器调用超类方法的特殊关键字。

    ex:
        // 调用父类的某个方法
        super.someMethod();
        // 调用父类的构造函数
        // 必须在子类构造函数的第一条语句调用
        super(arg1, arg2);
        // 如果子类构造器没有显试的调用超类的构造器，则将自动的调用超类默认(无参)的构造器。
        // 如果超类没有不带参数的构造器，并且在子类的构造器中又没有显试的调用超类
        // 的其他构造器，那么Java的编译器将报错。

    对比 this 和 super 

    this:

        1. 引用隐式参数。
        2. 调用该类其他的构造器。
        
    super:

        1. 调用超类的方法。
        2. 调用超类的构造器。
    
    两者在调用构造器时，调用语句都只能作为另一个构造器的第一条语句出现。
    构造参数既可以传递给本类(this)的其他构造器，也可以传递给超类(super)的构造器。

* 多态: 
    一个对象变量可以指示多种实际类型的现象叫做多态。

* 动态绑定:
    在运行时能够自动选择调用哪个方法的现象称为动态绑定。


### Object: 所有类的超类

* 如果一个类没有继承任何类，那么它默认继承的Object这个类。

* 在Java中，只有基本类型不是对象，ex: 数值、字符和布尔类型。
    所有的数组类型，都属于Object类的子类，不管是对象数组还是基本类型数组。

##### Object类的基本内容

* equals 方法: 

    用于检测一个对象是否等于另一个对象。(这里判断的是两个对象是否具有相同的引用)

* getClass 方法:

    返回一个对象所属于的类。

* 相等测试与继承

    * instanceof 进行检测，可能有子类，父类继承的关系，结果可能不准确。
    
    * Java语言要求 equals 方法具有以下特性:
    
        * 1.自反性: 对于任何非空引用x， x.equals(x) 应该返回 true.
        
        * 2.对称性: 对于任何应用x和y，当且仅当y.equals(x)返回true，
            x.equals(y)也返回true。

        * 3.传递性: 对于任何引用x、y和z，如果x.equals(y)返回true,
            y.equals(z)返回true,x.equals(z)也应该返回true。

        * 4.一致性: 如果x和y引用的对象没有发生变化，反复调用x.equals(y)应该
            返回同样的结果。

        * 5.对于任意非空引用x， x.equals(null)应该返回false.
        
    * 编写equals方法的建议:
    
        * 1.显式参数命名为otherObject，稍后将其传唤成另一个叫做other的变量。
        
        * 2.检测 this 与 otherObject 是否引用同一个对象:
            if(this == otherObject) return true;

        * 3.检测 otherObject 是否为 null, 如果为null，返回false。
            if(otherObject == null) return false;

        * 4.比较 this 与 otherObject 是否属于同一个类。如果 equals的语义在
            每个子类中有所改变，就使用getClass检测:
            if(getClass() != otherObject.getClass()) return false;
            如果所有的子类都拥有统一的语义，就使用 instanceof 检测:
            if(!(otherObject instanceof ClassName)) return false;

        * 5.将otherObject转换为相应的类类型变量:
            ClassName other = (ClassName)otherObject;

        * 6.对所有的域(属性)进行比较。使用 == 比较基本类型，
            使用 equals 比较对象域。如果所有域都匹配，返回true, 否则返回false。
            return field1 == other.field1
                && Objects.equals(field2, other.field2)
                && ...;

        如果子类中重新定义了equals，那么要调用 super.equals(other)。

        ** tips: **

        数组类型的域，可以使用静态的Arrays.equals方法检测相等。

        ** 记得在重写equals方法时，加上@Override注解。 **
        要不就是一个新方法，想想方法签名。

* hasCode 方法
    
    * hasCode方法，返回一个整型数值(也可以是负数)。
    
    * 如果重新定义了 equals方法，就必须重新定义hashCode方法。
    
    * hashCode方法定义在Object类中，每个对象都有一个默认的散列码，
        其值就是对象的存储地址。

    * 如果存在一个数组类型的域，可以使用静态的 Arrays.hashCode 方法计算一个散列码。
    
    * 可以调用Objects.hash并提供多个参数来生成散列值。
    
``` java
    public int hashCode()
    {
        return Objects.hash(name, year, sex);
    }
```
    
* toString 方法

    返回表示对象值得字符串。

* 部分API:
    
    * java.lang.Object 1.0
        
        * Class getClass()
            返回包含对象信息的类对象。

        * boolean equals(Object otherObject)
            比较两个对象是否相等，如果两个对象指向同一块存储区域，方法返回 true;
            否则返回false。在自定义的类中，应该覆盖这个方法。

        * String toString()
            返回描述该对象的字符串。在自定义的类中，应该覆盖这个方法。

    * java.lang.Class 1.0
        
        * String getName()
            返回这个类的名字。

        * Class getSuperclass()
            以Class对象的形式返回这个类的超类信息。


### 泛型数组列表





































