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

### 6. 删除分支

```
    git branch -d <branch-name>
    // 强行删除一个没有被合并过的分支
    git branch -D <branch-name>
```

### 7. 查看合并分支情况

```
    git log --graph --pretty=oneline --abbrev-commit
```

### 8. stash

```
    // 当前工作副本临时保存
    git stash
    // 所有 stash 的工作副本
    git stash list
    // 恢复工作副本(并不删除)
    git stash apply stash@{0}
    // 删除工作副本
    git stash grop stash@{0}
    // 恢复最近一次的工作副本, 并且删除该副本
    git stash pop
    
```

### 9. 与远程服务器

```
    // 查看远程服务器信息
    git remote -v
    // 将本地分支推送到远程服务器(本地不推送到远程服务器,别人看不到)
    // (如果失败可以先 git pull 从服务器上拉取新的提交)
    git push origin local-branch:remote-branch
    // 创建本地和远程对应的分支
    // (两者名称最好一直)
    git checkout -b branch-name origin/branch-name
    
    
```


