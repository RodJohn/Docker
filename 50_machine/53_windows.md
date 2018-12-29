# 示例

https://segmentfault.com/a/1190000005655288



Windows 10 安装 Docker for Windows 之后不能再安装 VirtualBox，
也就不能使用 virtualbox 驱动来创建 Docker Machine，
我们可以选择使用 hyperv 驱动。


docker-machine create -d hyperv test-hyperv

docker-machine create -d hyperv worker1

但是等很久，都不会下载成功，但是我们可以下载的网址复制下来，手动去下载，然后放到缓存目录

到docker for window软件的设置把运行的内存改成最小


可以在windowsHyper-V中查看
