# 索引

索引 是 **存储引擎** 用与快速找到记录的一种数据结构. 这是缩影最基本的功能.
    
    在 mysql 中, 存储引擎用类似的方法使用索引, 先在索引中找到对应的值, 
    然后根据这些值去找到对应的数据行. 
    
mysql 的索引的 **左原则**
    
    索引可以包含一个或多个列的值. 如果索引是多个列, 那么需要注意列的顺序, 
    因为 mysql 只能高效的使用 最左前缀列(重点).
    ex:
        index i_user_role (user_id, role_id)
        index i_role_user (role_id, user_id)
        i_user_role 和 i_role_user 是两个不同的索引, 例如
        select ... group by user_id,role_id --->use index i_user_role
        select ... group by role_id,user_id --->use index i_role_user
        select ... group by user_id --->use index i_user_role (左原则)
        select ... group by role_id --->use index i_role_user (左原则)


### 索引的类型
索引有很多种类型, 分别对应不同的场景提供更好的性能. mysql中的索引是存储引擎层实现的. 
不同的存储引擎对相同类型的索引在实现方式上可能也是不一样的

##### B-Tree索引 (B+Tree)
    
当人们谈论索引是, 并且没有特别的说明, 那么大部分说的就是这个. 主要讨论前 MyISAM 和 InooDB.
**B-Tree对索引列是顺序组织存储的.** (order by 的时候 就可能会用到所索引来排序,而不是内存排序)

    ps: 实际上很多存储引擎使用的是 B+Tree, 即每一个叶子节点都包含了一个指向下一个叶子节点的指针,
    方便叶子节点的遍历范围.
    
* MyISAM

    * 使用前缀压缩技术是索引更小
    * 使用的是数据的物理位置引用被索引的行
    
* InooDB

    * 按照原数据格式进行存储
    * 根据主见引用别索引的行