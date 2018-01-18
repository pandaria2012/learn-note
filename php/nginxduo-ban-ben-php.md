# nginx 多版本 php

### php7.2 官网下载 tar -xzvf ...

### 依赖  少什么  就安装什么
yum -y install readline-devel libxslt libxslt-devel

./configure --prefix=/usr/local/php72 \
--exec-prefix=/usr/local/php72 \
--with-config-file-path=/usr/local/php72/etc \
--enable-fpm \
--with-fpm-user=www \
--with-fpm-group=www \
--enable-inline-optimization \
--disable-debug \
--disable-rpath \
--enable-shared \
--enable-soap \
--with-libxml-dir \
--with-xmlrpc \
--with-openssl \
--with-mhash \
--with-pcre-regex \
--with-sqlite3 \
--with-zlib \
--enable-bcmath \
--with-iconv \
--with-bz2 \
--enable-calendar \
--with-curl \
--with-cdb \
--enable-dom \
--enable-exif \
--enable-fileinfo \
--enable-filter \
--with-pcre-dir \
--enable-ftp \
--with-gd \
--with-openssl-dir \
--with-jpeg-dir \
--with-png-dir \
--with-zlib-dir \
--with-freetype-dir \
--enable-gd-jis-conv \
--with-gettext \
--with-gmp \
--with-mhash \
--enable-json \
--enable-mbstring \
--enable-mbregex \
--enable-mbregex-backtrack \
--with-libmbfl \
--with-onig \
--enable-pdo \
--with-mysqli=mysqlnd \
--with-pdo-mysql=mysqlnd \
--with-zlib-dir \
--with-pdo-sqlite \
--with-readline \
--enable-session \
--enable-shmop \
--enable-simplexml \
--enable-sockets \
--enable-sysvmsg \
--enable-sysvsem \
--enable-sysvshm \
--enable-wddx \
--with-libxml-dir \
--with-xsl \
--enable-zip \
--enable-mysqlnd-compression-support \
--with-pear \
--enable-opcache

### 编译安装
make ZEND_EXTRA_LIBS='-liconv' && make install

### 拷贝相关文件
cp php.ini-production /usr/local/php72/etc/php.ini
cp /usr/local/php72/etc/php-fpm.conf.default  /usr/local/php72/etc/php-fpm.conf
cp /usr/local/php72/etc/php-fpm.d/www.conf.default  /usr/local/php72/etc/php-fpm.d/www.conf
cp sapi/fpm/init.d.php-fpm /etc/init.d/php-fpm72
cp sapi/fpm/init.d.php-fpm /usr/local/php72/bin/php-fpm72
chmod +x /etc/init.d/php-fpm72

### 配置别名
mkdir /usr/local/php72/bin/72
cp /usr/local/php72/bin/php /usr/local/php72/bin/72/php72
cp /usr/local/php72/bin/pecl /usr/local/php72/bin/72/pecl72
cp /usr/local/php72/bin/php-cgi /usr/local/php72/bin/72/php-cgi72
cp /usr/local/php72/bin/php-config /usr/local/php72/bin/72/php-config72
cp /usr/local/php72/bin/phpize /usr/local/php72/bin/72/phpize72

### 添加到环境变量
vim /etc/profile
PATH=$PATH:/usr/local/php72/bin/72
export PATH
### 使改动生效
source /etc/profile

### 修改相应的 pecl 配置 
pecl72 config-set php_ini /usr/local/php72/etc/php.ini	# 发现配置不生效
### ~/.pearrc 文件是 pecl 的配置文件的缓存文件, 其中的 php_ini 是安装完扩展后自动修改php.ini 项的    修改其值 可生效


### 安装 swoole 扩展
pecl72 install swoole

### 安装 memcached 扩展
yum install -y libmemcached-devel libmemcached
pecl72 install memcached 

    输入 libmemcached-dir  
    /usr

### 安装 event 扩展
pecl72 install event		# 全部默认值

### 安装 mongodb 扩展
pecl72 install mongodb

### 安装 rdkafka 扩展
pecl72 install rdkafka

### 安装 redis 扩展
pecl72 install redis
	# 会问是否开启压缩, 建议不开启   回车默认值

### 安装 mcrypt 扩展; 因为 php7.2 将 mcrypt 移除了核心包, mcrypt库很久没有更新了 官方建议用 open_ssl的
pecl72 install channel://pecl.php.net/mcrypt-1.0.1		# 回车默认值

### 安装 trie_filter.so 过滤敏感词库

    # 依赖 libdatrie 库 需要提前安装
    # 参考
    # https://github.com/zzjin/php-ext-trie-filter/tree/php7
    # 注意 phpize ---> phpize72; --with-php-config=/usr/local/php72/bin/php-config
    
    phpize72
    ./configure --with-php-config=/usr/local/php72/bin/php-config
    make && make install
    # 修改对应的 php.ini 添加 extension="trie_filter.so"


### 检查一下是否有错误 模块是否都正确安装了
php72 -m

### 修改 /usr/local/php72/etc/php-fpm.d 下的 www.conf 配置文件
大概 36 行
listen = /tmp/php-cgi72.sock

### 启动 php-fpm72
/etc/init.d/php-fpm72 start

### 配置 php-fpm72 开机自启
chkconfig --add php-fpm72
chkconfig php-fpm72 on
chkconfig 		# 检查一下

### nginx conf 文件夹下 添加 enable-php72.conf 内容如下

    location ~ [^/]\.php(/|$)
    {   
        fastcgi_index index.php;
        fastcgi_pass  unix:/tmp/php-cgi72.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
	# nginx -t ok  nginx reload

### 修改 php-cgi72.sock 的权限 和 所属组 所属者
chmod 755 /tmp/php-cgi72.sock
chown www:www /tmp/php-cgi72.sock

## ok了 