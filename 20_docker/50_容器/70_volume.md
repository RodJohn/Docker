


# 文件系统

    Docker镜像是由多个文件系统(只读层)叠加而成.
    当我们启动一个容器的时候,Docker会加载镜像层并在其上添加一个读写层.
    如果运行中的容器修改了现有的一个已存在的文件,
    那该文件将会从读写层下的只读层复制到读写层,该文件的只读版本仍然存在,只是已经被读写层中该文件的副本所隐藏.
    当删除Docker容器,并通过该镜像重新启动时,之前的更改将会丢失.
    在Docker中,只读层以及在顶部的读写层的组合被称为Union FIle System(联合文件系统).
    
# volume     

原理

    Volume指定目录或者文件,
    它可以绕过默认的联合文件系统,而以正常的文件或者目录的形式存在于宿主机上.
    就像一个docker和宿主机的同步文件夹
    
使用

    Volume可以使用下面两种方式创建:
    1.在Dockerfile指定VOLUME /some/dir
    2.执行docker run -v /some/dir命令指定        
    
# 示例

    docker run -it --name container-test -v /data ubuntu /bin/bash 

    使用docker inspect命令找到Volume在主机上的存储位置
    $docker inspect container-test  
        "Mounts": [  
            {  
                "Name": "6407cbb6700a4076cdeeef60629f1748ff34310102480a3f702fd3fee9e69134",  
                "Source": "/var/lib/docker/volumes/6407cbb6700a4076cdeeef60629f1748ff34310102480a3f702fd3fee9e69134/_data",  
                "Destination": "/data",  
                "Driver": "local",  
                "Mode": "",  
                "RW": true  
            }  
        ],  

    





# volume操作

删除

    删除容器,容器使用的volume并不会同时被删除.
    手动删除

备份    

    




# 共享Volume


    容器之间可以共享Volume
    
示例

    $docker run --name my_container -v /some/path ...  
    $docker run --volumes-from my_container --name my_contaner2 ...   
    Docker从第一个容器挂载相同的Volume到第二个容器,它可以在两个容器之间共享数据     