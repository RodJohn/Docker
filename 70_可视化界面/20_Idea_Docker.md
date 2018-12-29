
# 1 概述

    将idea作为客户端远程管理docker服务.


# 3 docker引擎设置


# 5 idea客户端设置
    

## 5.2 安装插件

    设置代理进行翻墙        
    安装 Docker Integration插件
    
    
## 5.3 设置docker服务

功能页面

    setting --> docker --> 选择+添加docker主机

设置
    
    选择tcp socket ,和默认url ,
    根据服务器情况设置证书文件
    
效果 
   
    设置成功可以看到connection successful 字样    
    
## 5.5 设置docker注册中心

    设置地址和验证信息



# 6 idea操作

## 6.1 进入界面

    view --> tool windows --> docker         
  
    
## 6.3 操作镜像


### pull push


### 创建并启动 * 

界面

    1.简单方式      
        界面--镜像右键创建
        功能--直接使用内置dockerfile启动
    2.多样启动
        界面--点击docker主机,选择deploy(左边菜单,三个箭头的图标)
        功能--可以选择dockerfile.dockercompose启动

参数设置

    选择服务器,镜像名,容器名
    配置dockerfile
    配置执行命令   
        直接写完整即可
    配置端口 
        填入hostport:containerport 

## 操作container

界面
    
    右键容器
    
操作

    inspect  查看容器Config
    exec     选择容器,输入命令  
           





# 参考

    http://blog.csdn.net/chenhaifeng2016/article/details/54315472
    http://blog.csdn.net/lovelife527386108/article/details/51697081
    https://www.cnblogs.com/hei12138/p/ideausedocker.html