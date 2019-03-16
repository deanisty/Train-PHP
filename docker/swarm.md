#### 理解集群

dokcer的集群就是一组运行docker的机器组成的一个集合。在集群中，所有的真实机器或者虚拟机器都被称作节点，使用常见的docker命令可以操作集群，但是，真正执行
命令的是集群管理器(swarm manager)，而不再是 docker 引擎。

集群管理器可以使用几种不同的策略运行容器，包括“最空节点策略” - 在闲置最久的机器上运行容器，或者“全局策略” - 保证置顶的容器的实例分布到每一台机器上。
通过在 Compose 文件中指定对应的策略。

集群管理器是集群中唯一能够执行命令的机器，并且它可以通过授权允许其他机器以 worker 的身份加入集群中。worker 们接受管理器的指令工作，不具备其他权限。

截止目前，Docker只是以单一主机的形式运行在本地机器中。但是它也可以切换到集群模式，切换到集群模式后会使当前主机变成集群管理器。然后所有执行的命令都会
在整个集群中起作用，而不是仅仅操作当前的机器。

#### 配置集群

集群是由多个节点组成的，节点可以是物理机器或者虚拟机。基本原理很简单：运行 `docker swarm init` 命令启用 swarm 模式并且设置当前机器为集群管理器，然后在其他机器上运行 `docker swarm join` 命令使之以 worker 的身份加入集群。

##### virtualbox

首先安装 virtualbox 用来创建虚拟机

[安装链接](https://www.virtualbox.org/wiki/Downloads)

使用 `docker-machine` 命令并已 virtualbox 作为驱动来制作虚拟机器

```SHELL
docker-machine create --driver virtualbox myvm1
docker-machine create --driver virtualbox myvm2
```

##### 获取虚拟机器列表和IP地址

```SHELL
docker-machine ls

$ docker-machine ls
NAME    ACTIVE   DRIVER       STATE     URL                         SWARM   DOCKER        ERRORS
myvm1   -        virtualbox   Running   tcp://192.168.99.100:2376           v17.06.2-ce
myvm2   -        virtualbox   Running   tcp://192.168.99.101:2376           v17.06.2-ce
```

##### 初始化集群并添加节点

第一个虚拟机器作为管理器，用于执行命令和授权其他机器加入集群，第二个虚拟机器作为worker。
You can send commands to your VMs using docker-machine ssh. Instruct myvm1 to become a swarm manager with docker swarm init and look for output like this:
通过运行 `docker-machine ssh` 发送命令到虚拟机中。首先通过 `docker swarm init` 设置 vm1为集群管理器，命令的输出如下：

```SHELL
$ docker-machine ssh myvm1 "docker swarm init --advertise-addr <myvm1 ip>"
Swarm initialized: current node <node ID> is now a manager.

To add a worker to this swarm, run the following command:

  docker swarm join \
  --token <token> \
  <myvm ip>:<port>

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
```

在第二个虚拟机上运行 `docker swarm join` 命令将其加入集群中

```SHELL
$ docker-machine ssh myvm2 "docker swarm join \
--token <token> \
<ip>:2377"

This node joined a swarm as a worker.
```

使用 `docker node ls` 命令可以列出刚才创建的节点

```SHELL
$ docker-machine ssh myvm1 "docker node ls"
ID                            HOSTNAME            STATUS              AVAILABILITY        MANAGER STATUS
brtu9urxwfd5j0zrmkubhpkbd     myvm2               Ready               Active
rihwohkh3ph38fhillhhb84sk *   myvm1               Ready               Active              Leader
```

在每个节点机器上运行 `docker swarm leave` 命令可以使其退出集群。
