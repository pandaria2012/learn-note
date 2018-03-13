### 数据类型

    java
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
                