### java的基本数据类型
    
    
    
    * 整型
        * int 4字节 -2147483648 ~ 2147483647 （-2^(4*8-1) ~ 2^(4*8-1)-1）
        * short 2字节 -32768 ~ 32767 （-2^(2*8-1) ~ 2^(2*8-1)-1）
        * long 8字节 -9223372036854775808 ~ 9223372036854775807 （-2^(8*8-1) ~ 2^(8*8-1)-1）
        * byte 1字节 -128 ~ 127（-2^7 ~ 2^7-1）
        
    * 浮点类型
        * float 4字节 有效位数为6~7位
        * double 8字节 有效位数为15位
        
        tips:
            正无穷大 (Double.POSITIVE_INFINITY, Float.POSITIVE_INFINITY)
            负无穷大 (Double.NEGATIVE_INFINITY, Float.NEGATIVE_INFINITY)
            NaN (Double.NaN, Float.NaN)
            一个正整数除以0为正无穷大，而 0/0 或者负数的平方根为 NaN；
            
    * char类型
        * 用来表示单个字符。通常用来表示字符常量。
            * 'A'和"A"表示的含义是不一样的，'A' 是编码为65所对应的字符常量，"A" 是一个包含A的字符串
        * 在java中，char类型用UTF-16编码描述一个代码单元。
    
    * boolean 类型
        * true
        * false
        
        tips:
            整型值和布尔值之间不能进行互相转换；
        
        