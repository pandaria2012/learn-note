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

