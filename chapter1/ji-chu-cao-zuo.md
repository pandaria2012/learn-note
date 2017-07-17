# a. 基础操作  {#a}

### 1. 创建版本库


```
    git init
    git add readme.md
    git commit -m 'wrote a readme.md'
```

### 2.查看当前状态


```
    git status
```


### 3.查看某个文件差异


```
    git diff readme.md
```


### 4. 版本回退


```
    // 回退到 commit_id 版本
    git reset --hard commit_id
    // 查看提交历史
    git log
    // 重返未来，回到未来的那个版本
    git reflog
```

### 5. 撤销修改

```
    // 放弃某个文件的修改 (未提交到远程仓库)
    git checkout -- filename
    // 回退版本， 并且放弃某个文件的修改(为提交到远程仓库)
    git reset HEAD filename
    git checkout -- filename
```

### 6. 删除文件

```
    
```

