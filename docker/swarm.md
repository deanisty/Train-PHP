#### 理解集群

dokcer的集群就是一组运行docker的机器组成的一个集合。在集群中，所有的真实机器或者虚拟机器都被称作节点，使用常见的docker命令可以操作集群，但是，真正执行
命令的是集群管理器(swarm manager)，而不再是 docker 引擎。

集群管理器可以使用几种不同的策略运行容器，包括“最空节点策略” - 在闲置最久的机器上运行容器，或者“全局策略” - 保证置顶的容器的实例分布到每一台机器上。
通过在 Compose 文件中指定对应的策略。

集群管理器是集群中唯一能够执行命令的机器，并且它可以通过授权允许其他机器以 worker 的身份加入集群中。worker 们接受管理器的指令工作，不具备其他权限。

截止目前，Docker只是以单一主机的形式运行在本地机器中。但是它也可以切换到集群模式，切换到集群模式后会使当前主机变成集群管理器。然后所有执行的命令都会
在整个集群中起作用，而不是仅仅操作当前的机器。

#### 配置集群

A swarm is made up of multiple nodes, which can be either physical or virtual machines. The basic concept is simple enough: run docker swarm init to enable swarm mode and make your current machine a swarm manager, then run docker swarm join on other machines to have them join the swarm as workers. Choose a tab below to see how this plays out in various contexts. We use VMs to quickly create a two-machine cluster and turn it into a swarm.
