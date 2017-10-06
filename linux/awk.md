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
        
        !~ 不匹配
        
        awk "$1/^a/{print NR,$1,$NF}" test.txt
        # 匹配 test.txt 文件的第一行的中的 以a开头的所有字段
        
        $1~/正则开始/,$3~/正则结束/
        

### awk常用内置变量

        RS        区分记录的分隔符
        FS        区分字段（域，列）
        $NF        最后一个字段
        NR        当前处理的行号
        ORS        输出时候的分隔符

### BEGIN 和 END

        
        BEGIN 在读取文件之前执行（初始化变量）
        
        END 在处理完文件后执行（统计用）
        
        awk 'BEGIN{print "hello wolrd!"}'
        
        awk '$0END{print "end!"}'


### awk数组



### 格式

        
        awk [ options ] 'pattern {action}' file 