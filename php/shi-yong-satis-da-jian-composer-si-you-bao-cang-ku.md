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
      "homepage": "http://packages.tuzuu.com",
      "repositories": [
        { "type": "git", "url": "http://git.tuzuu.com/duanbin/test.git" }
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
      需要被索引的git代码仓库地址
      
    * require
      需要被索引的包, 这里明确写明 可以减少 索引的内容
      
    * require-all
      这里如果不配置为 false 的话, 会索引全部的composer包(https://packagist.org/)

### 创建 索引

  php bin/satis build satis.json ./web -v #-v参数可以看到被索引的包