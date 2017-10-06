# AWK


### 字段（域）与记录

        $0 整行，一个记录
        $1 第一个字段
        $2 第二个字段
        ...
        $NF 最后一个字段
        以 FS 区分字段（域，列）
        以 RS 区分记录（行）
        
        

### 模式匹配
        
** 正则表达式 **
        
        awk "$1/^a/{print NR,$1,$NF}" test.txt
        # 匹配 test.txt 文件的第一行的中的 以a开头的所有字段
        
### 基本的awk执行过程


### awk常用内置变量

        RS        区分记录的分隔符
        FS        区分字段（域，列）
        $NF        最后一个字段
        NR        当前处理的行号
        ORS        输出时候的分隔符


### awk数组



### 格式

        
        awk [ options ] 'pattern {action}' file 