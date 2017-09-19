

 * mysql 主从复制之间默认的传输不是安全的, 非加密的.  主从复制之间可以搭建 ssl 链接.
   * 使用 mysql 内置的 ssl 链接. 需要 mysql 服务器在编译时支持ssl.
       
           master 配置
           [mysqld]
           ssl-capath=/etc/ssl/certs
           ssl-cert=/etc/ssl/certs/master.pem
           ssl-key=/etc/ssl/private/msater.key
           
           slave 配置
           slave > 
               CHANGE MASTER TO
               MASTER_HOST = 'master-1',
               MASTER_USER = 'repl_user',
               MASTER_PASSWORD = 'xyzzy',
               MASATER_SSL_CAPATH = '/etc/ssl/certs',
               MASTER_SSL_CERT = '/etc/ssl/certs/master.pem',
               MASTER_SSL_KEY = '/etc/ssl/private/msater.key';
           
           slave> START SLAVE;
   
  * 使用 stunnel 建立 ssl
      
          master 服务器配置文件  /etc/stunnel/master.conf
          cert=/etc/certs/master.pem
          key=/etc/ssl/private/master.key
          CApath=/etc/ssl/certs
          [mysqlrepl]
          accept=3508
          connect=3306
          
          3508 为 ssl 监听的端口(master 上 stunnel 监听的端口)
          3306 为 mysql 的端口(master 上 stunnel转接到此端口上)
          
          slave 服务器配置文件 /etc/stunnel/slave.conf
          cert=/etc/certs/slave.pem
          key=/etc/ssl/private/slave.key
          CApath=/etc/ssl/certs
          [mysqlrepl]
          accept=3408
          connect=master-1:3508
          
          3408 为 ssl 监听的端口(slave 上 stunnel 监听的端口)
          connect=master-1:3508 slave 上 stunnel 监听的本地 3408 端口后转发的端口 master-1 为 host
  
          slave 服务器
          slave > 
                  CHANGE MASTER TO 
                  MASTER_HOST = 'localhost',
                  MASTER_PORT = 3408,
                  MASTER_USER = 'repl_user',
                  MASTER_PASSWORD = 'xyzzy';
                  
          slave > START SLAVE;
          
* 注意 慎用 reset slave 它会删除 master.info 和 relay-log.info 以及所有的 中继日志文件! 
* master.info 上的配置信息 优先于 my.cnf
* master.info 和 relay-log.info 是 slave 用来保存 master 的信息 复制信息
* master.info 和 relay-log.info 有 配置文件来控制 my.cnf 
    
    
    relay-log-info-file=filename
    # 默认文件名为 relay-log.info
    
    master-info-file=filename
    # 默认文件名为 master.info

      
* slave 上的三个重要位置
    
    
    show slave status
    
    * Master_Log_File, Read_Master_Log_Pos
      mysql-bin.002583  310339097
      master 的读取位置: I/O线程即将从 master 二进制日志读取的下一个事件的位置.
      master.info 文件的第2, 3 行.
    * Relay_Master_Log_File, Exec_Master_Log_Pos
      mysql-bin.002583        310339097
      master 的执行位置: SQL线程即将执行的 master binlog 中下一个事件的位置.
      relay-log.info 文件的第 3 行
    * Relay_Log_File, Relay_Log_Pos
      slave-relay.001176   361
      中继日志的执行位置: SQL线程即将执行的 slave 中继日志中的下一个事件的位置.
      relay-log.info 文件的第 1, 2 行
      
 
 
 * slave 链接 master 的默认重连参数
     
     
     --slave-net-timeout
     默认 3600s
     --master-connect-retry
     default 60s
     --master-retry-count
     default 86400
     这个默认值最好重新改一下...太大了...
 
 
 * ** 基于行的复制 **
     
         binlog-format 参数
             
             STATEMENT 表示基于语句复制
             
             ROW 
             所有插入或改变数据的语句 使用基于行的复制 
             创建表或其他更改schema的语句还是 基于记录的复制
             
             MIXED 
             基于语句复制的安全版本 --- 混合模式
             如果写入二进制日志的语句是不安全语句, 则切换为基于行复制
             ex: 
                 UUID函数
                 用户自定义函数
                 同一个语句更改了两张或多张 含有 auto_increment 列的表
             
         binglog-max-row-event-size
             控制事件大小, 处理行复制时不会消耗太多内存.
 
          
          