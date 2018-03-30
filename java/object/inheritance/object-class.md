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
