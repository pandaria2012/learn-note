

* 修改和删除时 要小心

* 删除用户
    
    
    不能确认用户相关目录有没有重要数据的 不能用 userdel -r 
    userdel -r 删除用户并且删除家目录
    
    一般：
    1. vim /etc/passwd, 然后注释掉用户
    2. 把登录 shell 改成 /sbin/nologin
    3.openldap(类似活动目录) 账号同意管理的，ladp库里干掉用户。
        所有服务器全部都没了。
        
        

* 某个进程只存在一个(shell)


    processNum = `ps aux | grep DaemonExportMissions | grep -v "grep" | grep -v "sh" | wc -l`
    if [$processNum -eq 0 ];then
        nohup /usr/local/php/bin/php /home/www/Public/index.php DaemonExportMissions >> /var/logs/worker/DaemonExportMissions.log 2>/dev/null&
    fi 
    
    
    
