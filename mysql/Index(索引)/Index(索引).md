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
