### 反射

能够分析类能力的程序称为反射。
反射可以用来:
    * 在运行中分析类的能力。
    * 在运行中查看对象，例如，编写一个toString方法供所有类使用。
    * 实现通用的数组操作代码。
    * 利用Method对象，这个对象很像c++中的函数指针。
对于构造工具非常有用。

##### Class类

* Object类中的getClass()方法将会返回一个Class类型的实例。
``` java
    // Object类中的getClass()方法
    Date d;
    ...
    Class cl = d.getClass();

    // 也可以调用静态方法forName获得类名对应的Class对象
    String className = "java.util.Date"
    Class.forName(className);
    // 这个方法只有在className是类名或接口名时才能够执行，否则将抛出异常
```

* Class类相关Api

    * java.lang.Class 1.0 
        
        * static Class forName(String ClassName)
        
            返回描述类名为className的Class对象。

        * Object newInstance()
    
            返回这个类的一个新实例

        * Field[] getFields() 1.1 
        * Field[] getDeclaredFields() 1.1 
        
            getFields方法将返回一个包含Field对象的数组，这些对象记录了这个类或
            其超类的公有域。getDeclaredField方法也将返回包含Field对象数组，这些
            对象记录了这个类的全部域。如果类中没有域，或者Class对象描述的是基本
            类型或数组，将返回长度为0的数组。

        * Method[] getMethods() 1.1 
        * Method[] getDeclareMethods() 1.1
            
            返回包含Method对象的数组：getMethods将返回所有的公有方法，包括从超
            类继承来的公有方法;getDeclaredMethods返回这个类或接口的全部方法，但
            不包括由超类继承了的方法。 

        * Constructor[] getConstructors() 1.1 
        * Constructor[] getDeclaredConstructors() 1.1
        
            返回包含Constructor对象的数组，其中包含了Class对象所描述的类的所有公有构造器(getConstructors)或所有构造器(getDeclaredConstructors)。 

    * java.lang.reflect.Constructor 1.1 
        
        * Object newInstance(Object[] args)
        
            构造一个这个构造器所属类的新实例。
            args: 提供给构造器的参数
    
    * java.lang.reflect.Field 1.1 
    * java.lang.reflect.Method 1.1
    * java.lang.reflect.Constructor 1.1 
    
        * Class getDeclaringClass()
        
            返回一个用于描述类中定义的构造器、方法或域的Class对象。

        * Class[] getExceptionTypes() (在Constructor和Method类中)
        
            返回一个用于描述方法抛出异常类型的Class对象数组。

        * int getModifiers()
        
            返回一个用于描述构造器、方法或域的修饰符的整型数值。使用Modifier类
            中的这个方法可以分析这个返回值。

        * String getName()
        
            返回一个用于描述构造器、方法或域名的字符串。

        * Class[] getParameterTypes() (在Constructor和Method类中)
        
            返回一个用于描述参数类型的Class对象数组。

        * Class getReturnType() (在Method类中)
        
            返回一个用于描述返回类型的Class对象。

    * java.lang.reflect.Modifier 1.1 
    
        * static String toString(int modifiers)
        
            返回对应modifiers中位设置的修饰符的字符串表示。

        * static boolean isAbstract(int modifiers)
        * static boolean isFinal(int modifiers)
        * static boolean isInterface(int modifiers)
        * static boolean isNative(int modifiers)
        * static boolean isPrivate(int modifiers)
        * static boolean isProtected(int modifiers)
        * static boolean isPublic(int modifiers)
        * static boolean isStatic(int modifiers)
        * static boolean isStrict(int modifiers)
        * static boolean isSynchronized(int modifiers)
        * static boolean isVolatile(int modifiers)
        
            检测方法名中对应的修饰符在modifiers值中的位。