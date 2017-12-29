# docker 下搭建运行 gitlab 


    sudo docker run -i \
    --hostname gitlab.pandamonk.com \
    -p :443:443 -p :80:80 -p :222:22 \
    --name gitlab \
    --restart always \
    --volume /home/conf/gitlab/config:/etc/gitlab \
    --volume /home/conf/gitlab/logs:/var/log/gitlab \
    --volume /home/conf/gitlab/data:/var/opt/gitlab \
    --volume /home/conf/gitlab/logs/reconfigure:/var/log/gitlab/reconfigure \
    gitlab/gitlab-ce:latest && docker exec -it gitlab update-permissions && docker restart gitlab
    


### 配置文件
    
    