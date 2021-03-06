#### 特点

* Flexible: Even the most complex applications can be containerized.
* Lightweight: Containers leverage and share the host kernel.
* Interchangeable: You can deploy updates and upgrades on-the-fly.
* Portable: You can build locally, deploy to the cloud, and run anywhere.
* Scalable: You can increase and automatically distribute container replicas.
* Stackable: You can stack services vertically and on-the-fly.

#### 映像文件和容器

容器是通过运行映像文件启动的。映像文件是可执行的，包括了运行一个应用程序所需要的一切：代码、运行时、库文件、环境变量和配置文件。
一个容器是影响文件的一个运行的实例 -- 它是由映像文件在内存中执行时产生的，也就是一个拥有状态或者用户进程的映像文件。
在 linux 系统中可以通过 docker ps 命令查看当前运行的容器列表。

#### 容器和虚拟机

当一个容器在 Linux 系统中运行，它和其他容器共享操作系统。它运行在一个独立的进程中，不会占用比其他可执行文件更多的内存，所以它更轻量级。

相比之下，一个虚拟机运行在一个完整的操作系统中（可以被称为访客操作系统），并且通过超级监管器访问虚拟系统资源。
通常情况下，虚拟机提供的资源比一个应用程序运行时需要的多。


#### 容器-服务-栈

> 译至 ： https://docs.docker.com/get-started/part2/

Docker把应用程序分成三个层次，至下往上分别是：容器(container)、服务(services)、栈(stack)

过去，如果你想要用 Python 编写app，你必须要首先安装 python ，搭建开发环境，而且要保证 python 的版本符合你的需要，并且开发环境要和生成环境保持一致。
但是，有了 docker 之后你只需要下载一个可移植的 python 镜像，无需安装，只需要保证 python 镜像和你的app一起被构建，这样你的 app，以及它需要的依赖，
运行时时刻都在一起。这种可移植的镜像被一种称为 Dockerfile 的东西定义。

##### 使用 Dockerfile 定义容器

Dockerfile 定义容器的运行环境。容器环境虚拟化了对网络接口和硬盘驱动的访问，并且和系统的其他部分隔离开，所以需要用端口号和容器外的环境做映射，还可以
指定复制哪些文件到容器环境中。通过这些操作，使用 dockerfile 定义的 app 环境可以在任何地方构建，并且保持一致的运行效果。

##### Dockerfile

```SHELL
# User an official Python runtime as a parent name
FROM python:2.7-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

##### (Services) Docker Compose

讲解服务，如何将 app 规模化并实现负载均衡。

* 什么是服务

分布式应用程序中，程序的不同部分被称为服务。例如，一个视频分享网站，可能会包含存储应用数据到数据库中的服务、用户上传后在后台做视频转码的服务、前端
服务等等。

服务就是“产品中的容器”。一个服务只包含一个映像文件，但是它限制了映像文件的运行方式 ： 使用哪个端口、为了保持服务所需的规模容器可以运行多少副本，等。
服务的规模影响运行指定软件的容器实例的个数，同时也影响进程中分配给服务的计算资源的多少。

在 docker 中通过使用 docker-compose.yml文件定义、运行和扩展服务的规模。

##### docker-compose.yml file

```SHELL
version: "3"
services:
  web:
    image: username/repo:tag   # 替换成自己的映像文件名
    deploy:
      replicas: 5
      resources:
        limits:
          cpus: "0.1"
          memory: 50M
      restart_policy:
        condition: on-failure
    ports:
      - "4000:80"
    networks:
      - webnet
networks:
  webnet:
```

启动服务

```SHELL
docker swarm init

docker stack deploy -c docker-compose.yml getstartedlab

```


检查启动状态

```SHELL
#检查当前启动的服务
docker service ls
#检查指定名称的服务状态
docker service ps getstartedlab_web

docker container ls -q
```

运行在一个服务中的容器被称作一个任务。任务拥有递增的唯一ID，对应在 docker-compose.yml 中指定的复制的个数。使用下面的名列出服务的任务：

```SHELL
docker service ps getstartedlab_web
```

任务也可以通过列出系统中的容器展示出来，但是没有通过服务分组：

```SHELL
docker container ls -q
```

可以通过多次执行 curl -4 http://localhost:4000命令或者在浏览器中访问链接查看返回的id.

```SHELL
Hello World!
Hostname: 9710352b8a98
Visits: cannot connect to Redis, counter disabled
```

从返回的id可以看出，负载均衡起到了作用，id一直在变化，每次请求，5个任务中的某一个被选中，并且返回的id和前面命令返回的id一致。
To view all tasks of a stack, you can run docker stack ps followed by your app name, as shown in the following example:
还可以通过下面的命令查看任务堆栈：

```SHELL
docker stack ps getstartedlab
```

##### 改变应用的规模

通过修改 docker-compose.yml 文件中的replicas的值可以改变应用的任务数量，修改并保存后，重新执行 `docker stack deploy` 命令：

```SHELL
docker stack deploy -c docker-compose.yml getstartedlab
```

Docker执行就地更新，不需要重建任务堆栈或者杀死容器进程。

##### 关闭应用程序和集群（swarm）

执行 `docker stack rm` 命令移除堆栈

```SHELL
docker stack rm getstartedlab
```

关闭集群：

```SHELL
docker swarm leave --force
```


