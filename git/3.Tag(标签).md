# Tag(标签)

    tag 和 commit 一一对应的关系
    标签也是版本库的一个快照



### 1. 创建标签

```
    // 打在最近一次 commit 上的
    git tag <tag-name>
    
    //打在某个 commit 上的
    git tag <tag-name> commit_id
    
    // 创建带说明的标签: -a <tag-name> -m 'some commit'
    git tag -a v0.1 -m 'version 0.1 released' commit_id
    
    // 用私钥签名一个标签 -S
    // 签名采用 PGP 签名, 因此, 必须首先安装gpg(GunPG). 
    //如果没有赵高gpg, 或者没有gpg 秘钥对, 就会报错
    git tag -s v0.1 -m 'signed version 0.2 released' commit_id
    
```


### 2. 查看标签

```
    // 列出所有标签
    git tag
    // 查看某个标签
    git show <tag-name>
```


### 3. 删除标签

```
    // 删除本地标签
    git tag -d <tag-name>
    // 推送某个标签到远程服务器
    git push origin <tag-name>
    // 推送所有的标签到远程服务器
    git push origin --tags
    
    // 删除远程服务器上的某个标签
    // a. 先删除本地的
    git tag -d <tag-name>
    // b. 再删除远程服务器上的某个标签
    git push origin :refs/tags/<tag-name>
```

