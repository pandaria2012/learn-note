# docker 下搭建 mysql


* /etc/docker/daemon.json

        {
          "registry-mirrors": ["https://registry.docker-cn.com"]
        }


* docker 运行容器命令

    docker run -i -t centos /bin/bash


* 总是自动重启这个容器

    docker run -i -t --restart=always centos /bin/bash


* 要下载 docker hub mysql 官方镜像

    docker pull mysql


* docker 容器内 运行的 mysql 数据保存的地方, 数据不要保存在 docker 的容器内 要保存在 物理机器上
    
    
    # 物理机地址
    /data/docker_mysql_data/master01

* 配置启动 mysql 的配置文件
    
    
    # mysql 配置文件目录
    /data1/docker_mysql_data/master01/conf

* master 的配置


    # mysql配置文件
    /data1/docker_mysql_data/master01/conf/my.cnf

* 数据库文件  数据 二进制log 存放位置

    
    # 数据库 数据存放的 物理机位置
    /data1/docker_mysql_data/master01/data

    chmod -R 777 /data1/docker_mysql_data

* 创建 容器 并运行 


    docker run -d -P --name master01 -p :3506:3306 -e mysqld -e MYSQL_ROOT_PASSWORD=root -e MYSQL_USER=bearcat -e MYSQL_PASSWORD=root  -e MYSQL_DATABASE=bearcat -v /data1/docker_mysql_data/master01/data:/var/lib/mysql -v /data1/docker_mysql_data/master01/conf:/etc/mysql/conf.d  mysql
    
    # 命令解释


* ip 端口 

        master01		172.17.0.2:3306	3506
        slave1001		172.17.0.3:3306	3507
        slave1002		172.17.0.4:3306	3508
        mysqlrouter	        172.17.0.5:7001	7001	172.17.0.5:7002	7002

* mysql-router	默认config_folder
    
    
    # mysql router 配置文件 物理机位置
    /usr/local/etc/mysqlrouter

    docker run -it --name mysqlrouter -p :7001:7001 -p :7002:7002 -v                 /data1/docker_mysql_data/mysqlrouter/conf:/usr/local/etc/mysqlrouter centos


* 容器内启动 mysql router


    /usr/local/mysqlrouter/bin/mysqlrouter -c /usr/local/etc/mysqlrouter/mysqlrouter.conf &














