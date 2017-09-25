# 常用命令

## 常见通配符

* >
* \>>
* <
* <<

## 目录相关

* cd 

* pwd

* mkdir

* rmdir

## 文件与目录管理

* ls

* cp

* rm

* mv

* rename

## 文件相关

* cat

* tac

        将cat命令的输出结果 反过来

* rev

        将每一行的结果反过来输出

* nl

* more

* less

* tail

* head

* touch

* od

## 目录与文件 权限相关命令

** 特殊权限 SUID, SGID, SBIT **

* umask

* chattr 改变文件属性
    
        # 给 test.txt 加上 追加属性
        # test.txt 文件 只可以被追加进内容
        chattr +a test.txt  
        
        # 给文件加锁
        #不允许修改 删除 test.txt文件
        chattr +i test.txt
        
* lsattr 显示文件的扩展属性

        lsattr test.txt
        
* chmod

* chown

* chgrp

## 查找文件或目录

* which

* whereis

* locate

* find

## 用户, 用户组

#### 用户

* useradd （etc/passwd,/etc/shadow /etc/group /etc/gshadow）

* userdel（etc/passwd,/etc/shadow /etc/group /etc/gshadow）

* chage (/etc/passwd)

        设置或修改用户密码有效期限
        
        查看用户信息
        -l www
        修改用户账户过期时间
        -E "2018/01/02" www
        ...

* usermod 修改用户信息

* passwd (/etc/shadow)

* id

* chfn

* chsh 

#### 用户组

* groupadd (/etc/group)

* groupdel

* groupmod

* gpasswd

* groups

* grpck

* grpconv

* grpunconv

#### 在登录的用户信息

* w

* who

* last

* lastlog

* write

* mesg

* wall

* mail

#### 检查工具

* pwck

* pwconv

* pwunconv

* chpasswd

#### 切换身份 或 获取超级权限

* su -

* sudo

* visudo

echo

cut











