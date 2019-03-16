#### 什么是 stack

栈是分布式应用中最高层的概念。栈是一组相互关联的共享依赖的服务，并且可以被一起编排和管理。一个单独的栈可以定义和整合一个完整的应用的功能，尽管许多复杂的
应用可以使用多个栈。

当创建一个 Compose 文件和使用 `docker stack deploy` 命令时就已经在使用栈了。但是栈不仅仅只运行在一台机器中，它可以在多台机器中，并且有多个服务互相
关联。

#### 创建一个新的服务并且重新部署。

在 `docker-compose.yml` 文件中新增一个服务visualizer，visualizer 是一个可以查看当前集群中容器状态的项目

```SHEll
version: "3"
services:
  web:
    image: deepdoo/get-started:part2
    deploy:
      replicas: 5
      restart_policy:
        condition: on-failure
      resources:
        limits:
          cpus: "0.1"
          memory: 50M
    ports:
      - "80:80"
    networks:
      - webnet
  visualizer:
    image: dockersamples/visualizer:stable
    ports:
      - "8080:8080"
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
    deploy:
      placement:
        constraints: [node.role == manager]
    networks:
      - webnet
networks:
  webnet:
```

保存 compose 文件并重新部署

```SHELL
重新启动集群
docker swarm init 
重新部署
$ docker stack deploy -c docker-compose.yml getstartedlab
Updating service getstartedlab_web (id: angi1bf5e4to03qu9f93trnxm)
Creating service getstartedlab_visualizer (id: l9mnwkeq2jiononb5ihz9u7a4)
```

访问 8080 端口就可以看到 visualizer 的输出，包含当前 web 容器的数量和 visualizer 本身的一个容器。
正如 composer 文件中限定的一样，visualiser 容器运行在集群管理器机器中，而 web 服务的5个容器实例平均分配到集群的其他机器中。
可以使用 `docker stack ps` 命令来证实这一点

```SHELL
docker stack ps getstartedlab
```

visalizer 是一个单例服务可以运行在服务栈中任何能够包含它的应用里。它不依赖任何其他东西。接下来要创建的Redis 服务，与之相反，它是有依赖的服务。

#### 增加 redis 服务

修改 compose 文件如下

```SHELL
version: "3"
services:
  web:
    image: deepdoo/get-started:part2
    deploy:
      replicas: 3
      restart_policy:
        condition: on-failure
      resources:
        limits:
          cpus: "0.1"
          memory: 50M
    ports:
      - "80:80"
    networks:
      - webnet
  visualizer:
    image: dockersamples/visualizer:stable
    ports:
      - "8080:8080"
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
    deploy:
      placement:
        constraints: [node.role == manager]
    networks:
      - webnet
  redis:
    image: redis
    ports:
      - "6379:6379"
    volumes:
      - "/home/docker/data:/data"
    deploy:
      placement:
        constraints: [node.role == manager]
    command: redis-server --appendonly yes
    networks:
      - webnet
networks:
  webnet:
  
```

Redis拥有一个官方的docker镜像文件，并且被允许使用 redis 作为短名称，所以不需要 用户名/仓库名 的惯例前缀。6379端口是redis 的默认端口号，容器中的redis
会把这个端口号暴露给容器所在的机器， compose 文件的配置允许机器将此端口暴露到外部，所以通过任一节点的IP地址都可以进入 Redis 管理工具来管理容器中的
redis.

在部署服务栈的过程中，关于redis还要一些事项需要注意

* redis 总是运行在管理器机器中，所以它总是使用相同的文件系统
* redis 总是访问容器中的 /data 目录，并且在那里保存数据

因此如果没有为 redis 指定保存数据的真实物理空间，当运行 redis 的容器被销毁时，redis 保存的数据也会消失，所以 compose 文件保证了以下两点：


* placement 指令限制了 redis 容器总是使用同一个机器
* volume 指令将 redis 容器的 /data 目录映射到主机的 ./data 目录并允许其访问，因此在 redis 容器启动和终止过程中，redis 保存的数据不会丢失


##### 创建 data 目录

```SHELL
mkdir ./data
```

##### 重新部署服务栈

```SHELL
docker stack deploy -c docker-compose.yml getstartedlab
```

##### 查看服务

```SHELL
docker service ls
```

##### 访问 80 端口查看 redis 保存数据

自己看

##### 访问 8080 端口查看 visualizer

自己看
