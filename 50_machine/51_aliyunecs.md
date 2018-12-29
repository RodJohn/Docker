#阿里云docker-machine

# 教程

https://yq.aliyun.com/articles/6809?spm=5176.10695662.1996646101.searchclickresult.21ec08b6omlJcO
# github
https://github.com/AliyunContainerService/docker-machine-driver-aliyunecs
bug
https://github.com/AliyunContainerService/docker-machine-driver-aliyunecs/issues/21


# 我的实践

1.安装驱动

    下载驱动,重命名,放置在bin目录中
    
2.设置秘钥

    export ECS_ACCESS_KEY_ID='<Your access key ID>'
    export ECS_ACCESS_KEY_SECRET='<Your secret access key>'
    注意=号前后空格
    
3.创建虚拟机

    docker-machine create -d aliyunecs  --aliyunecs-instance-type=ecs.n1.tiny  --aliyunecs-io-optimized=optimized  dev1
    注意驱动类型,实例类型,io优化,地区
    
    