# Docker

[TOC]

### 0.组件｜元素

```
Docker Client：用户和 Docker 守护进程进行通信的接口，也就是 docker 命令。
Docker 守护进程：宿主机上用于用户应答用户请求的服务。
Docker Index：用户进行用户的私有、公有 Docker 容器镜像托管，也就是 Docker 仓库。

Docker 容器：用于运行应用程序的容器，包含操作系统、用户文件和元数据。
Docker 镜像：只读的 Docker 容器模板，简言之就是系统镜像文件。
DockerFile：进行镜像创建的指令文件。
```



### 1.image

```
docker images
docker pull <image name>
```



### 2.container

```
docker ps 【-a】
docker exec -it 4  (exit)
docker [container] stop CONTAINER_ID
docker rm CONTAINER_ID
```





### 3.repository