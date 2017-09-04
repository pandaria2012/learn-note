# 配置复制

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
        










