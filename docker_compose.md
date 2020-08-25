# Docker Compose手册

## DockerCompose的用途

docker-compose是docker用于定义和运行拥有多个容器的docker应用的管理工具。

docker-compose使用yaml文件作为配置的描述文件。

docker-compose可以同时工作于：
	生产、开发、测试、CI工作流等环境。

要启动用docker-compose管理的docker应用，可以用命令 docker-compose up

## docker-compose配置文件格式

我们主要聊的是docker-compose-file 2.0格式的配置文件。

docker-compose-file 2.0 格式需要docker 1.10 以上支持。

为了docker-compose能知道当前配置文件的格式是2.0，我们需要在docker-compose-file的yml文件
中的第一行中指定docker-compose-file的版本。

	version: "2.0"

因为docker-compose认为一个docker应用是由多个services组成的。
所有docker-compose-file的核心配置节点就是services。

## SERVICES

services节点下是每个服务的容器启动配置，节点名为服务名。

每个service下的配置与docker run的参数基本对应。

### image
image标签是用于指定运行容器的起始镜像的。

	image: <镜像标签>|<镜像哈希>

### container_name
用于指定运行容器的名称

	container_name: <容器名称>


### ports
用于映射主机端口到容器内端口

	ports:
	  - <主机端口>:<容器内端口>


### volumes
用于映射主机路径到容器内路径
	
	volumns:
	  - <主机路径>:<容器内路径>
	  
### restart
用于设定容器的重启策略。容器缺省的重启策略是：不重启。

	restart: no|always|on-failure[：max-retries]|unless-stopped

* no: 表示容器退出后，docker服务不会自动重启容器
* on-failure[:max-retires]: 表示容器在容器中的主应用在以非零的异常状态退出后，docker服务会进行最大max-retries次重启容器操作。
* always: always表示docker服务只要发现容器不在启动状态，立刻重启服务。也就是说，在always状态的容器，即便服务器重启后也会自动重启。
* unless-stopped: 除非人工stop了，或是docker服务被停止了或重启了，容器都会被重启。



