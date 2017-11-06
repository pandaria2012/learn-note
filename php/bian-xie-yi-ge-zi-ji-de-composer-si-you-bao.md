# 编写一个 自己的 composer 私有包

### 在 gitlab 上 创建一个项目 clone到本地

    git clone http://git.pandamonk.com/pandamonk/test.git
    cd test


### 目录结构

    .
        src
            SayHello.php


### SayHello.php 的文件内容
    
    <?php
    /**
     * this is a test for composer package.
     * Date: 2017/11/3
     * Time: 16:51
     */
    
    namespace Hello;
    
    class SayHello {
    
    
        public static function world () {
    
            return 'Hello World!';
        }
    
    }
    
    

### 生成  composer.json 文件
    
    // 切换到包的根目录下, 执行
    composer init
    
    // 根据相应的提示 来生成 项目的 composer.json文件
                                      
    Welcome to the Composer config generator  
                                                
    
    
    This command will guide you through creating your composer.json config.
    
    Package name (<vendor>/<name>) [root/composer-car]: pandamonk/hello
    Description []: This a demo for build composer packagist .
    Author [pandamonk <pandamonk@xxx.com>, n to skip]: 
    Minimum Stability []: dev
    Package Type (e.g. library, project, metapackage, composer-plugin) []: library
    License []: MIT
    
    Define your dependencies.
    
    Would you like to define your dependencies (require) interactively [yes]? no
    Would you like to define your dev dependencies (require-dev) interactively [yes]? no
    
    {
        "name": "pandamonk/hello",
        "description": "This a demo for build composer packagist.",
        "type": "library",
        "license": "MIT",
        "authors": [
            {
                "name": "pandamonk ",
                "email": "pandamonk@xxx.com"
            }
        ],
        "minimum-stability": "dev",
        "require": {}
    }
    
    Do you confirm generation [yes]? yes
    Would you like the vendor directory added to your .gitignore [yes]? yes
    
    // 再次 目录结构
    .
        composer.json
        src
            SayHello.php


### 需要手动编辑一下 composer.json文件

    {
        "name": "pandamonk/hello",
        "description": "This a demo for build composer packagist.",
        "type": "library",
        "license": "MIT",
        "authors": [
            {
                "name": "pandamonk ",
                "email": "pandamonk@xxx.com"
            }
        ],
        "minimum-stability": "dev",
        "require": {},
        "autoload": {
            "psr-4": {
                "Hello\\": "src/"
            }
        }
    }
    
    
### 现在 手动测试一下 刚写好的 composer 包


      // 切换到包的根目录
      composer install
      // 目录结构
      .
          composer.json
          composer.lock
          src
              SayHello.php
          vendor
              autoload.php
              composer
              
              
      // 在包的根目录下 新建一个测试文件 test.php
      <?php  
        require_once __DIR__ . '/vendor/autoload.php';  
        use Hello\SayHello;  
        echo SayHello::world();
    
    在项目根目录下执行命令  php test.php
   
### 将写好的 包 发送到  gitlab 上

     首先在  项目根目录下 的 .gitignore 文件中 将
     verdor/*
     composer.lock 
     加入其中 
     
     git add .
     git commit -m 'some commit'
     git push
     
    //  最好打上 tag 也推送过去
    git tag 1.0.1 -a -m 'v1.0.1 release'
    git push --tags 