# 常用命令

## 常见通配符

* \>
* \>\>
* \<
* \<<
* \*
* \!

## 命令行常用快捷键

* ctrl + 左右键 ---> 在单词间跳转

* ctrl + a ---> 行首

* ctrl + e ---> 行尾

* ctrl + k ---> 剪切光标后面的内容

* ctrl + u ---> 剪切整行的内容

* ctrl + l ---> 清屏

* ctrl + y ---> 粘贴 (ctrl + k 或 ctrl + u )的内容

* ctrl + w ---> 删除光标前面的 一个 单词 (空格区分)

* ctrl + h ---> 删除光标左边的字符

* ctrl + d ---> 删除光标右边的字符

* !! ---> 执行上一条命令

* ctrl + p 显示当前命令的上一条命令

* ctrl + r ---> 搜索历史命令

* ctrl + s ---> 阻止屏幕输出

* ctrl + q ---> 允许屏幕输出

* ctrl + c ---> 终止命令

* ctrl + z ---> 挂起命令

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

#### 在登录的用户

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


## shell 相关

* echo

* alias

* unalias

* history

* seq 序列

## 多用于管道中

#### 截取

* cut

* grep

#### 排序

* sort    sort lines of file 


        -k2 按照第二列排序（默认空格分隔符分隔列）

* uniq        滤重（默认 相邻的滤重 并非全局的）

* wc 统计文件行数  单词数  字节数  字符数 

#### 双向重导向

* tee

#### 字符转换

* tr

* col

* join

* paste    merge line of files
        
        -d 分隔符
        -s 行转换成列

* expand

#### 分割(文件或文件内容)

* split -l n input_file output_file


    # 指定行数
    -l n input
    # 指定生成文件后缀行数
    -a n
    ... 
#### 参数替换

* xargs

## 磁盘相关

* df -hT -i inode

* du

* fdisk 分区

* mkfs 格式化磁盘

* fsck 磁盘检验 (没坏的磁盘一定不要用)

* badblocks  磁盘检验(没坏的磁盘一定不要用)

* mount 挂载

* umount 卸载 -lF 强制卸载

* partprobe 把分区表的修改变化通知内核

* mkswap 格式化 swap 分区

* swapon/swapoff 使用 swap 分区， ex: 是外婆呢、dev/sdb1

* dumpe2fs 查看 ext 文件系统信息

* parted 分区工具 (常用大于2T）

* tune2fs 修改文件系统信息

* megacli 查看 raid xinxi 

* ipmitools 查看硬件信息

* resize2fs 调整文件系统大小 （LVM,drbd）








