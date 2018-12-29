
# 概述

    用于自动化定制镜像

# 基础设置 

## FROM *

	指定基础镜像
	FROM 是必备的指令，并且必须是第一条指令。
	
## MAINTAINER 

    用于指定镜像创建者和联系方式。 
    MAINTAINER <author name> 	

# VOLUME *

    定义匿名卷
    向匿名卷写入的信息都不会记录进容器存储层
    
    
# COPY *

作用

    文件复制
    将从构建上下文目录中 <源路径> 的文件/目录复制到新的一层的镜像内的 <目标路径> 位置
    源文件的各种元数据都会保留。比如读、写、执行权限、文件变更时间等
    
格式：

    COPY <源路径>... <目标路径>
    

## WORKDIR

    WORKDIR /path/to/work/dir 配合 RUN，CMD，ENTRYPOINT 命令设置当前工作路径。
    可以设置多次，如果是相对路径，则相对前一个 WORKDIR 命令。默认路径为/。

# ENV 

设置环境变量
格式有两种：

ENV <key> <value>
ENV <key1>=<value1> <key2>=<value2>...    
    
# ADD

作用 
    
    ADD 指令和 COPY 的格式和性质基本一致
    但是
    <源路径> 是URL，Docker会试图去下载这个链接的文件放到 <目标路径> 去。下载后的文件权限自动设置为 600，
    <源路径> 是tar 压缩文件的话，压缩格式为 gzip, bzip2 以及 xz 的情况下，ADD 指令将会自动解压缩这个压缩文件到 <目标路径> 去。

    在 COPY 和 ADD 指令中选择的时候，所有的文件复制均使用 COPY 指令，仅在需要自动解压缩的场合使用 ADD。

# EXPOSE


作用

    EXPOSE 指令是声明运行时容器提供服务端口，
    这只是一个声明，在运行时并不会因为这个声明应用就会开启这个端口的服务。
    一个是帮助镜像使用者理解这个镜像服务的守护端口，以方便配置映射；
    一个用处则是在运行时使用随机端口映射时，会自动随机映射 EXPOSE 的端口。    
    
格式：

    EXPOSE <端口1> [<端口2>...]
    



  

# RUN *

作用

	RUN 指令是用来执行命令的。

格式

    shell 格式：
        RUN <命令>，就像直接在命令行中输入的命令一样。
        RUN echo '<h1>Hello, Docker!</h1>' > /usr/share/nginx/html/index.html
    exec 格式：
        RUN ["可执行文件", "参数1", "参数2"]，
        这更像是函数调用中的格式。
    注意,空格    

格式说明

    推荐使用 exec 格式，
    这类格式在解析时会被解析为 JSON 数组，因此一定要使用双引号 "，而不要使用单引号。
    如果使用 shell 格式的话，实际的命令会被包装为 sh -c 的参数的形式进行执行。比如：
    CMD echo $HOME 在实际执行中，会将其变更为 CMD [ "sh", "-c", "echo $HOME" ]

特别的

    Docker 不是虚拟机，容器中的应用都应该以前台执行，而不是像虚拟机、物理机里面那样，用 upstart/systemd 去启动后台服务，容器内没有后台服务的概念。
    一些初学者将 CMD 写为：
    
    CMD service nginx start
    然后发现容器执行后就立即退出了。甚至在容器内去使用 systemctl 命令结果却发现根本执行不了。这就是因为没有搞明白前台、后台的概念，没有区分容器和虚拟机的差异，依旧在以传统虚拟机的角度去理解容器。
    
    对于容器而言，其启动程序就是容器应用进程，容器就是为了主进程而存在的，主进程退出，容器就失去了存在的意义，从而退出，其它辅助进程不是它需要关心的东西。
    
    而使用 service nginx start 命令，则是希望 upstart 来以后台守护进程形式启动 nginx 服务。而刚才说了 CMD service nginx start 会被理解为 CMD [ "sh", "-c", "service nginx start"]，因此主进程实际上是 sh。那么当 service nginx start 命令结束后，sh 也就结束了，sh 作为主进程退出了，自然就会令容器退出。
    
    正确的做法是直接执行 nginx 可执行文件，并且要求以前台形式运行。比如：
    
    CMD ["nginx", "-g", "daemon off;"]    




# 默认目标进程 *

    用于设置默认进程
    因为启动容器的追踪目的就是运行某个进程
    一个 Dockerfile 中只能有一个，如果有多个，则最后一个生效。

## CMD

作用
    
    指定容器默认启动的进程
    但如果在运行时指定的命令会替代掉这个默认命令

格式

    CMD 指令的格式和 RUN 相似，也是shell和exec两种.
    

## ENTRYPOINT *

作用

    ENTRYPOINT 的目的和 CMD 一样，都是在指定容器启动程序及参数。
    特点1
        在运行时指定的命令会作为该默认命令的新的参数
    特点2    
        当指定了 ENTRYPOINT 后，CMD 的含义就发生了改变，
        不再是直接的运行其命令，而是将 CMD 的内容作为参数传给 ENTRYPOINT 指令，
        换句话说实际执行时，将变为：<ENTRYPOINT> "<CMD>"

    
    
示例

    ENTRYPOINT [ "java","-jar","app.jar" ]    

