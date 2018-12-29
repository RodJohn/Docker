

# 参考

    http://portainer.readthedocs.io/en/stable/deployment.html
    
    http://blog.csdn.net/a22698488/article/details/54911419
    https://blog.csdn.net/csdn_duomaomao/article/details/73380395



# 3 安装监控机

原理
    
    监控机也是一个docker进程
    这个进程监控指定的docker引擎
    并提供可视化的web服务
    
操作
    
    docker run -d --privileged -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v /opt/portainer:/data portainer/portainer

开启页面

    http://DOCKER_HOST:9000
    提示添加用户
    此时已经添加本机为监控机


# 5 单机操作

## 创建容器

    很方便
    

# 7 swarm 

service
    
    