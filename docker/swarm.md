#### 理解集群

dokcer的集群就是一组运行docker的机器集合在一个群里。在集群中，所有的真实机器或者虚拟机器都被称作节点，使用常见的docker命令可以操作集群，但是，真正执行
命令的是集群管理器(swarm manager)，而不再是 docker 引擎。

Swarm managers can use several strategies to run containers, 
such as “emptiest node” -- which fills the least utilized machines with containers. 
Or “global”, which ensures that each machine gets exactly one instance of the specified container. 
You instruct the swarm manager to use these strategies in the Compose file, just like the one you have already been using.

Swarm managers are the only machines in a swarm that can execute your commands, or authorize other machines to join the swarm as workers. 
Workers are just there to provide capacity and do not have the authority to tell any other machine what it can and cannot do.

Up until now, you have been using Docker in a single-host mode on your local machine. 
But Docker also can be switched into swarm mode, and that’s what enables the use of swarms. 
Enabling swarm mode instantly makes the current machine a swarm manager. 
From then on, Docker runs the commands you execute on the swarm you’re managing, rather than just on the current machine.
