# sed


** 语法格式 **

    
    sed [options] [sed-commands] [input-file]
    
    
    
### 增删改查

#### 增
** 一次可以追加多行内容(使用 \n) **
* a 在第几行后追加内容
    
    
    # 在第二行后追加内容
    sed '2a abc,abc,abc' test.txt
    
* i 在第几行前插入内容

    
    # 在第二行前插入内容
    sed '2i abc,abc,abc' test.txt
    
    
##### 关于 '第几行' 的更多写法

    
    # n1, n2 可以是数字, 正则表达式, 或者二者的组合
    n1[,n2]{sed-commands}
    ex:
        10{sed_commands}
        10,20{sed_commands}
        10, +20{sed_commands}
        10, ${sed_commands}
        1~2{sed-commands}    对1,3,5,7,……行操作
        /something/{sed_commands}
        /something/, /anotherthing/{sed_commands}
        /something/, ${sed_commands}
        /something/,10{sed_commands}
        1, /anotherthing/{sed_commands}
        /something/, +2{sed_commands}


#### 删

删除匹配的行

* d


#### 改

* c   按行来替换   一行一行的替换


    sed '2c abc,abc,abc' test.txt

* s(g)    搜索替换
    
    
    # 加上 g 是每行的全局替换,   不加 g 是只替换匹配到的每行的第一个元素
    # # 为定界符   可以随便换
    
    sed 's#something#replacement#g' test.txt
    
    # something 这里的 something 可以是正则表达式 非常强大
    # replacement 中可以用 & 来表示 所有搜索到的符合 something 的值
    # 同样也支持  正则表达式里的反向引用 ()  \1


    
#### 查

* p    
    
    
    # 使用方法跟 i a c 相似
    
    sed -n '2p' test.txt
    
    # 这里加上 -n 选项  如果不加上 -n 选项会输出所有内容 和 匹配到的内容
    # -n 选项表示只输出 匹配到的内容

    
    
    
    
    
    
    
    
    
    
    