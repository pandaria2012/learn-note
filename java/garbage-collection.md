# JAVA 的垃圾回收机制

** HotSpot虚拟机 **


### 分代收集

        在 java 堆区可以被分为 新生代(YoungGen) 和 老年代(OldGen), 新生代又细分为 Eden 空间, 
    From Survivor空间, 和 To Survivor 空间.
    
   
   ![](/assets/java内存堆区图.png)
   
           java 堆区内存图
           

### 垃圾标记: 根搜索算法


        以根对象集合作为起始,按照从上至下的方式搜索被根对象集合所连接的目标对象是否可达, 不可达说明
    目标对象已经死亡.将其标记为垃圾对象


![](/assets/根搜索算法.png)


### 区域化分代式: G1(Garbage-Frist)收集器
将全堆扫描,改为堆内的块扫描.

        初始标记:
                标记 Root-Region
        根区域扫描:
                扫描 Root-Region 中引用的老年代的一些 Region 块(不会执行新生代内存回收,程序hang住)
        并发标记:
                找出整个 java 堆区中的存活对象(交叉执行新生代内存回收)
        再次标记:
                整个 java 堆区中存活对象标记(程序hang住)
        清除:
                计算活跃对象,并完全释放一些自由的Region块(程序hang住),然后处理
                Remembered Set(程序hang住), 并发重置一些空闲Region块,并放回至空闲列表.
        拷贝:
                将存活的对象,复制到未使用过的Region块中.(程序hang住)


![](/assets/基于Region块的java堆区布局.png)