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


## 索引的类型
索引有很多种类型, 分别对应不同的场景提供更好的性能. mysql中的索引是存储引擎层实现的. 
不同的存储引擎对相同类型的索引在实现方式上可能也是不一样的

#### B-Tree索引 (B+Tree)
    
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
    
**左原则说明**

    1. 如果不是按照索引的最左列开始查找, 则无法使用索引.
    
        ex: 
        
            index i_user_role (user_id, role_id)
            select ... where role_id = 100 用不到 i_user_role 索引
            
    2. 不能跳过索引中的列
            
            ex:
                index i_user_role_permission (user_id, role_id, permission_id)
                select ... where user_id = 100 and permission_id = 50
                只能用到 i_user_role_permission 索引的 user_id 列
            
    3. 查询中有某个列的范围查询
            
            
            ex:
                index i_name_first_last (first_name, last_name)
                select ... where first_name='%c' and last_name='Bob'
                无法使用索引 i_name_first_last
            
            
##### 哈希索引 (hash index)
mysql中 只有**Memory**引擎支持, 也是 Memory引擎的默认索引类型

    ps: Memory支持非唯一哈希索引, 如果多个列的哈希值相同, 
    索引会以链表的方式存放多个记录指针到同一个哈希条目中.
    


##### 空间索引 (R-Tree)
MyISAM表支持空间索引, 可以用作地理数据存储.
GIS解决方案做得好的是 PostgreSQL 的 PostGIS.


##### 全文索引 (不支持中文)
match aganst 操作

    ex: where MATCH(field1, field2, ...) AGANST('\*word\*' IN BOOLEAN MODE) 

mysql5.6的 InooDB 开始支持 这种索引.(还是不支持中文)
替代方案  **Sphinx** 


##### 其他类型的索引
其他存储引擎使用不同的数据结构来存储索引

            
     
            
## 索引的优点
 
    * 大大减少服务器需要扫描的数据量
    * 可以帮助服务器避免排序和临时表
    * 可以将随机i/o 变为 顺序i/o
    
    
##### 一个索引是否适合某个查询的 "三星系统"

* 一星: 索引将相关的记录放到一起 (注意左原则)
* 二星: 索引中的数据顺序和查找中的排列顺序一致 (order by 语句)
* 三星: 索引中包含了查询中需要的全部列 (索引覆盖或覆盖索引)

##### 索引是 "银弹" 吗?

    当索引帮助存储引擎快速查找到到记录带来的好处大于其带来的额外工作是, 索引才是有效的.
    对于数据量少的小表, 全表扫描获取更高效点.
    对于中大型的表, 索引会比较高效.
    对于特大型的表, 建立和使用索引的代价会非常高, 可以使用分区 在或者上大数据集群
    

    



    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
            
            
            
            
            
            
            
            
            