### 枚举类

```
// 声明一个枚举类：简单方式
public enum Size { SMALL, MEDIUM, LARGE, EXTRA_LARGE };

// 也可以在美剧类型中添加一些构造器、方法、域。
public enum Size
{
    SMALL("S"), MEDIUM("M"), LARGE("L"), EXTRA_LARGE("XL");

    private String abbreviation;

    private Size(String abbreviation){ this.abbreviation = abbreviation; }
    public String getAbbreviation() {return abbreviation;}
}
// 使用方法
{
    Size size = Enum.valueOf(Size.class, "SMALL");
    System.out.println("size=" + size);
    System.out.println("abbreviation=" + size.getAbbreviation());
    System.out.println(size == Size.EXTRA_LARGE);
}

```

* API: java.lang.Enum<E> 5.0

    * static Enum valueOf(Class enumClass, String name)
    
        返回指定名字、给定类的枚举常量。

    * String toString()
    
        返回枚举常量名。

    * int ordinal()

        返回枚举常量在enum声明中的位置，从0开始计数。

    * int compareTo(E other)

        如果枚举常量出现在other之前，返回一个负值; 如果 this == other 返回0;
        否则返回正值。枚举常量的出现次序在enum声明中给出。