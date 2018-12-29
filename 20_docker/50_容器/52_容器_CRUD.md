
# 新建并启动

命令

    docker run <option>

运行过程

    检查本地是否存在指定的镜像，不存在就从公有仓库下载
    利用镜像创建并启动一个容器
    分配一个文件系统，并在只读的镜像层外面挂载一层可读写层
    和dockerfile的关系
    从宿主主机配置的网桥接口中桥接一个虚拟接口到容器中去
    从地址池配置一个 ip 地址给容器
    执行用户指定的应用程序
    执行完毕后容器被终止


常用参数

    -d  让 Docker 在后台运行
    	启动后会返回一个唯一的 id    

    -t  分配输出终端
    
    -i  保持输入打开

示例

```
输出一个 “Hello World”，之后终止容器。
    $ docker run ubuntu:14.04 /bin/echo 'Hello world'
    Hello world


启动一个 bash 终端，允许用户进行交互。
    $ docker run -t -i ubuntu:14.04 /bin/bash
    root@af8bae53bdd3:/#
    其中，-t 选项让Docker分配一个伪终端（pseudo-tty）并绑定到容器的标准输入上，
     -i 则让容器的标准输入保持打开。


后台运行
    $ docker run -d ubuntu:17.10 /bin/sh -c "while true; do echo hello world; sleep 1; done"
    77b2dc01fe0f3f1265df143181e7b9af5e05279a884f4776ee75350ea9d8017a
```



# 查看

命令

	docker container ls 
	查看运行的容器,注意NAMES在最后一行
	相当于docker ps  
	
参数

    -a	查看全部的容器 

示例

```
docker ps -a
CONTAINER ID        IMAGE                    COMMAND                CREATED             STATUS                          PORTS               NAMES
ba267838cc1b        ubuntu:14.04             "/bin/bash"            30 minutes ago      Exited (0) About a minute ago                       trusting_newton
98e5efa7d997        training/webapp:latest   "python app.py"        About an hour ago   Exited (0) 34 minutes ago                           backstabbing_pike
```


# 终止

强制终止命令
    
    docker container stop  <NAMES>

自动终止条件

	1.用户指定的应用完成时
	2.用户通过 exit 命令或 Ctrl+d 来退出终端时



# 删除

删除终止的容器   

    docker container rm <NAMES>
    如果要删除一个运行中的容器，可以添加 -f 参数

删除全部终止的容器   

    docker container prune



# 其他操作 

启动终止的容器

    docker container start <NAMES>
    
重启运行的容器   

    docker container restart <NAMES>





