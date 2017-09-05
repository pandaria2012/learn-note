# 配置复制 - 全新的开始

### 配置master

* master 开启二进制日志
* 全局唯一的服务器ID
* 在 master 创建一个拥有复制权限的复制用户

配置文件加入以下配置项:

```
    ...
    [mysqld]
    ...
    ...
    log-bin = master-bin
    log-bin-index = master-bin.index
    server-id = 1    #此id最好做好规划
    ...
    ...
```

关于 log-bin 的文件名, 其默认值是 hostname-bin. 如果系统的主机名改了, 那么log-bin的名称也会随着改变(但是
mysql 依然可以通过 log-bin-index 索引文件获取正确的二进制日志文件). 但是最好还是这是一个与服务器无关的唯一
文件名, 防止该来该去很混乱. 

在 master 上创建一个复制用户:

```
    master>
        CREATE USER repl_user;
    master>
        GRANT REPLICATION SLAVE ON *.* TO repl_user IDENTIFIED BY 'xyzzy';
```

重启 master 使配置生效

### 配置slave

* slave 开启中继日志
* 全家唯一的服务器ID

配置文件加入以下配置项:

```
    ...
    [mysqld]
    ...
    ...
    server-id = 2    #此id最好做好规划
    relay-log-index = slave-relay-bin.index
    relay-log = slave-relay-bin
    ...
    ...
```

关于 relay-log 的文件名, 基本与 log-bin 文件名规则一致. 但是 ** 如果主机名改变了, mysql 将无法
找到中继日志索引文件, 而认为中继日志为空. **

重启 slave 使配置生效


### 链接 master 和 slave

```
    slave> 
        CHANGE MASTER TO 
        MASTER_HOST = 'master-1', 
        MASTER_PORT = 3306, 
        MASTER_USER = 'repl_user, 
        MASTER_PASSWORD = 'xyzzy'; 
        
    slave> 
        START SLAVE;
```


### 清空, 重新开始
    
```
    -- 清空 slave 上相关表 --
    STOP SLAVE;
    RESET SLAVE;
    -- 清空 master 上相关表 --
    RESET MASTER;
```
** RESET MASTER **: 删除所有二进制日志文件并清空二进制日志索引文件.
** RESET SLAVE **: 删除 slave 复制所用的文件.
    注意:
        * 在执行 RESET MASTER 时, 确保没有任何 slave 链接到 master 上.
        * 在执行 RESET SLAVE 时, 先执行 STOP SLAVE 命令, 确保 slave 上没有活动的复制.
        



# 配置复制 -- 中途复制

如果没有开启二进制日志, 先开启二进制日志.
并给所有表加锁. (数据完整, 防止在备份期间有新数据写入.)
    master > FLUSH TABLES WITH READ LOCK;
锁定表后, 找出当前正在使用的二进制日志文件及其binlog位置.
    master > SHOW MASTER STATUS;
记录下下一个事件的位置: File: master-bin.000042, Position: 456552 .这就是复制的起点, 
这个位置点之前的数据都在备份里.
接下来就是创建备份了.
    mysqldump --all-databases --host=master-1 > backup.sql
备份完成后, 释放锁.
    master > UNLOCK TABLES;
然后在 slave 上恢复备份的数据.
    mysql --host=slave-1 < backup.sql
然后启动 slave 服务, 并配置复制信息.
    slave > CHANGE MASTER TO 
    MASTER_HOST = 'master-1', 
    MASTER_PORT = 3306, 
    MASTER_USER = 'slave-1',
    MASTER_PASSWORD = 'xyzzy', 
    MASTER_LOG_FILE = 'master-bin.000042', 
    MASTER_LOG_POS = 456552;
开启复制
    slave > START SLAVE;

tips:
    mysqldump 命令
    --master-data =  1 / 2:
        = 1: 导出文件里会有 CHANGE MASTER TO ...语句 .
        = 2: 导出文件里会有 CHANGE MASTER TO ...语句, 但是被写成了一个 SQL 注释, 提供信息.
        默认值是 1.
    --single-transaction
        在开始dump备份的时候开启一个事务, 并设置事务隔离级别为可重复读.
        但是不影响其他数据的写入更新删除等操作.但是修改表结构的语句不能执行, 
        如 ALTER TABLE, DROP TABLE 等语句.
        此参数对支持事务的存储引擎有用.
    
# 配置复制 -- 从已有的 slave 上备份数据, 配置新的 slave

停止 slave
    slave-1 > STOP SLAVE;
查看当前 slave 的状态
    slave-1 > SHOW SLAVE STATUS;
拿到当前 slave 同步的 master 的 log file, 和 position. 
    Relay\_Master\_Log\_File: master-bin.000042
    Exec\_Master\_Log\_Pos: 546632
备份当前 slave(slave-1) 上的数据.
在新的 slave(slave-2) 上恢复备份的数据.
在新的 slave 上配置复制信息:
    slave-2 > CHANGE MASTER TO
            MASTER_HOST = 'master-1',
            MASTER_PORT = 3306,
            MASTER_USER = 'slave-1',
            MASTER_PASSWORD = 'xyzzy',
            MASTER_LOG_FILE = 'master-bin.000042',
            MASTER_LOG_POS = 546632;
开启复制
    slave-2 > START SLAVE;


