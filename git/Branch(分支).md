# Branch(分支)


### 1. 查看分支

```
    git branch
```


### 2. 创建分支

```
    git branch <branch-name>
```


### 3. 切换分支

```
    git checkout <branch-name>
```

### 4. 创建 + 切换分支

```
    git checkout -b <branch-name>
```

### 5. 合并某分支到 __当前分支上__

```
    // fast forward 合并模式
    git merge <branch-name>
    // 普通合并模式
    git merge --no-ff -m 'some comments' dev
```

### 6. 