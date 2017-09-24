# 常用命令



## 常见通配符

* >
* \>>
* <
* <<

cd 

pwd

echo

ls

cat

tac
    
    将cat命令的输出结果 反过来

rev

    将每一行的结果反过来输出

rm

mv

mkdir

rename

chmod

chown

chgrp

passwd (/etc/shadow)

cut

more

less

tail

head

useradd （etc/passwd,/etc/shadow /etc/group /etc/gshadow）

userdel（etc/passwd,/etc/shadow /etc/group /etc/gshadow）

chage (/etc/passwd)
设置或修改用户密码有效期限
    
    查看用户信息
    -l www
    修改用户账户过期时间
    -E "2018/01/02" www
    ...
    

usermod 修改用户信息

id

w

who

last

lastlog

su

sudo

visudo

find

groupadd (/etc/group)

groupdel

groupmod

groups

grpck

grpconv

grpunconv

cp

chattr 改变文件属性
    
    # 给 test.txt 加上 追加属性
    # test.txt 文件 只可以被追加进内容
    chattr +a test.txt  
    
    # 给文件加锁
    #不允许修改 删除 test.txt文件
    chattr +i test.txt  

lsattr 显示文件的扩展属性

    lsattr test.txt