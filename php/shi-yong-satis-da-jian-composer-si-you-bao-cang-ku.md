# 使用 satis 结合 gitlab 搭建 composer 私有包仓库


### 环境

    centos 7.3
    composer
    gitlab
    nginx


### 使用  安装 satis 

    composer create-project composer/satis --keep-vcs
    
### 配置 satis.json
    
    {
      "name": "tuzuu",
      "homepage": "http://packages.pandamonk.com",
      "repositories": [
        { "type": "git", "url": "http://git.pandamonk.com/pandamonk/test.git" }
      ],
      "require-all": false,
      "require-dependencies": true,
      "require-dev-dependencies": true,
      "require": {
        "pandamonk/hello": "*"
      },
      "archive": {
        "directory": "dist",
        "format": "zip",
        "skip-dev": true
      },
      "config": {
        "secure-http": false
      }
    }
    
    * homepage 
      私有 composer 包管理的 url地址
      
    * repositories
      需要被索引的git代码仓库地址 这里引用的是  gitlab 的 地址
      
    * require
      需要被索引的包, 这里明确写明 可以减少 索引的内容
      
    * require-all
      这里如果不配置为 false 的话, 会索引全部的composer包(https://packagist.org/)

### 创建 索引

    php bin/satis build satis.json ./web -v #-v参数可以看到被索引的包
    
### 定时更新 
  
    crontab 执行  创建索引命令 
    
### 使用 docker 搭建 nginx 环境, 访问 satis 的composer 本地私有库

    // 临时关闭 selinux, 否则 docker 在挂载 volume 是会有文件权限问题
    setenforce 0
    // 拉取 nginx 镜像
    docker pull nginx
    
    // 拷贝nginx 镜像中的 默认的 nginx 部分配置文件
    docker run --name tmp-nginx-container -d nginx
    docker cp tmp-nginx-container:/etc/nginx/conf.d/ /etc/nginx/conf.d/
    docker rm -f tmp-nginx-container
    
    // 修改 conf.d/default.conf 文件 的 server_name 值为  satis.json 中 homepage 的值
    server_name  packages.pandamonk.com;
    
    // 开启 nginx 镜像
    docker run --name nginx --restart always -p :80:80 -v /root/test/my-satis/web:/usr/share/nginx/html:ro -v /etc/nginx/conf.d/:/etc/nginx/conf.d/ -d nginx
    
    -v /root/test/my-satis/web:/usr/share/nginx/html:ro   挂载 satis 生成的静态文件
    -v /etc/nginx/conf.d/:/etc/nginx/conf.d/ nginx 的 vhost 文件目录
    
    // 大功告成 浏览器 访问 
    http://packages.pandamonk.com
    
    
