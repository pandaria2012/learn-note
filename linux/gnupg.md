## GUNPG(gpg)

#### 安装

    centos 下直接使用 yum 安装
    yum install gnupg

    安装完成后，可以查看帮助命令
    gpg --help

#### 生成秘钥

```
    gpg --gen-key
    * 回车后会先让你选择秘钥的种类 (默认用RSA 来加密和签名)
    * 然后会问你秘钥的长度 (默认2048位，越长越安全)
    * 设定秘钥的有效期 (0表示永不过期)
    * 确认以上信息 y/n 
    * 填写个人信息：真实姓名，电子邮件，注释
    * o 再次确认信息
    * 询问是否需要生成一个密码来保护你的秘钥(程序内使用的话，不要填写这个密码，
        程序内无法访问命令行。。。)
    * 等待。。。。很漫长(程序会建议你敲打键盘，移动鼠标，读写硬盘等等)

```

#### 撤销证书
    以后密钥作废时，可以请求外部的公钥服务器撤销你的公钥。

```
    gpg --gen-revoke [user_id]
```

#### 列出秘钥

```
    gpg --list-keys
```

#### 删除秘钥

```
    gpg --delete-key [user_id]
```

#### 导出秘钥

```
    gpg --armor --output public-key.txt --export [user_id]
    gpg --armor --output private-key.txt --export-secret-keys [user_id]
```

#### 上传公钥

```
    gpg --send-keys [user_id] --keyserver hkp://subkeys.pgp.net

    // 生成公钥指纹
    gpg --fingerprint [user_id]
```

#### 导入秘钥

```
    gpg --import [秘钥文件]

    // 可以让对方直接给你公钥， 也可以到公钥服务器上寻找公钥
    gpg --keyserver hkp://subkeys.pgp.net --search-keys [user_id]
    // 这里不能保证公钥的可靠性
```

#### 加密与解密

```
    // 加密一个文件
    gpg --recipient [user_id] --output demo.en.txt --encrypt demo.txt
    // recipient: 指定接受这的公钥
    // output: 指定加密后的文件名
    // encrypt: 指定源文件

    // 解密
    gpg --decrypt demo.en.txt --output demo.de.txt 
    // decrypt: 需要解密的文件
    // output: 解密后生成的文件
    // 解密的简写方式
    gpg demo.en.txt // 直接显示在标准输出当中
```

#### 签名

```
    // 对文件进行签名
    gpg --sign demo.txt 
    // 会在当前目录下生成 demo.txt.gpg文件，默认是二进制存储的文件
    gpg --clearsign demo.txt 
    // 会在当前目录下生成 demo.txt.asc文件，是ASCII码形式的文件。

    // 如果想要将签名文件和文件内容分开放
    gpg --detach-sign demo.txt 
    // 当前目录下生成一个单独的签名文件demo.txt.sig。同样默认二进制形式
    gpg --armor --detach-sign demo.txt
    // 生成ASCII码形式的签名文件
```


#### 同时签名与加密

```
    gpg --local-user [sender_id] --recipient [receive_id] --armor --sign --encrypt demo.txt
    // local-user: 发信者私钥签名
    // recipient: 接收者公钥加密
    // armor:采用ASCII码形式显示
    // sign: 表示需要签名
    // encrypt: 表示指定源文件
```

#### 验证签名

```
    gpg --verify demo.txt.asc demo.txt 
```

## 在PHP中使用

#### 环境

```
    centos 需要安装 gpgme gpgme-devel
    yum install gpgme gpgme-devel
    php 需要 gnupg 扩展
    pecl install gnupg
```

#### 加解密(签名验证)前置步骤

``` php
    // 在linux中， 在生成key的时候，可以加上 --homedir /path/to/your/project
    // 然后将此目录的所有者所属组改为相应的值(一般是www:www)
    // 如果是从别的机器上拿的私钥公钥，要导入到自己的机器上
    // 并且导入的时候也建议加上 --homedir /path/to/your/project
    // 并修改相应的权限
    // gpg --homedir /path/to/your/project --import private-key.txt

    // php gnupg 可以使用面向对象和函数式两种方式

    // 可选 配置 GNUPGHOME 环境变量，.gnupg 目录的位置
    // 在 new \gnupg()之前(gnupg_init())设置，
    // FPM/FastCGI/Module 模式下的php 需要对此目录有写权限，否则后续都会报错
    putenv('GNUPGHOME=/var/www/vhosts/yourdomain/.gnupg');

    // 实例化一个 gnupg 对象
    $gpg = new \gnupg();
    // 设置错误异常
    $gpg->seterrormode(GNUPG_ERROR_EXCEPTION);
    // 设置 签名方式 (签名和原文件分离，一个单独的签名文件或签名字符串)
    $gpg->setsignmode(GNUPG_SIG_MODE_DETACH);
    
    // $keyinfo 可以查看所有的生成或导入的 key的信息
    // 这里需要取出所需要私钥和公钥的fingerprint
    // 可以写在配置里 也可以从 $keyinfo 数组中取出
    $keyinfo = $gpg->keyinfo('');

    // 拿到相应的 $private_key_info 来做签名或加密
    // 添加签名key， $res-> 是否成功
    $res = $gpg->addsignkey($private_key_info['fingerprint']);
    // 签名, $sign是签名结果，成功返回签名，失败 try catch错误
    $sign = $gpg->sign('this is a text');



    // 验证签名, $info 签名结果，可以跟private_key_info 中的相应值做比较
    // 看是否有改动 (fingerprint对比)
    $info = $gpg->verify($signed_text,$signature);
    $info[0]['fingerprint'] == $private_key_info['fingerprint'];
```



















