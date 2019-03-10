#### Docker

##### 安装 

https://docs.docker.com/install/linux/docker-ce/centos/

##### 设置普通用户运行 docker

https://docs.docker.com/install/linux/linux-postinstall/

##### 概念

```shell
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
 ```

* 客户端和后台进程通信
* 后台进程从映像站拉取映像文件
* 后台进程通过映像文件创建一个新的容器，容器中运行的可执行文件产生输出内容
* 后台进程通过数据流把输出传输给客户端
