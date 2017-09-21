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

passwd

cut

more

less

tail

head

useradd

userdel

chage

usermod

id

su

sudo

visudo

find

groupadd

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