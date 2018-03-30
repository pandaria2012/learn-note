
### 泛型数组列表

ArrayList<T>类，a = b，a和b引用同一个数组列表。(ArrayList<Type> b = ArrayList<>())

* API: java.util.ArrayList<T> 1.2
    
    * ArrayList<T>()
    
        构造一个空列表数组。

    * ArrayList<T>(int initialCapacity)
    
        用指定容量构造一个空数组列表。
        initialCapacity: 数组列表的最初容量

    * boolean add(T obj)
        
        在数组列表的尾端添加一个元素。永远返回true。
        obj: 添加的元素

    * int size()
    
        返回存储在数组列表中的当前元素数量。(这个值小于等于数组列表的容量。)

    * void ensureCapacity(int capacity)
    
        确保数组列表在不重新分配存储空间的情况下就能够保存给定数量的元素。
        capacity: 需要的存储容量

    * void trimToSize()
        
        将数组列表的存储容量消减到当前尺寸。

    * void set(int index, T obj)
        
        设置数组列表指定位置的元素值，这个操作将覆盖这个位置的原有内容。
        index: 位置(在 0 ~ size()-1 之间)
        obj: 新的值

    * T get(int index)
        
        获得指定位置的元素值
        index: 获得的元素位置(在 0 ~ size()-1 之间)

    * void add(int index, T obj)
        
        向后移动元素，一遍插入元素。
        index: 插入位置(在 0 ~ size()-1 之间)
        obj: 新元素

    * T remove(int index)
    
        删除一个元素，并将后面的元素向前移动。被删除的元素由返回值返回。
        index: 被删除的元素位置(在 0 ~ size()-1 之间)


* 访问数组列表元素
    
    * get(index) // 返回值为Object，注意接收值后要强转。
    * set(index, value) // 注意index必须被初始化过(或是有值)，否则应用add()。

