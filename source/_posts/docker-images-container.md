---
title: docker使用镜像和操作容器
date: 2018-08-24 17:34:27
tags:
---

## 使用镜像

### 拉取镜像

Docker Hub 上有大量的镜像可以用，从 Docker 镜像仓库获取镜像的命令是 docker pull。其命令格式如：

```
$ docker pull ubuntu
```

对于 Docker Hub，如果不给出用户名，则默认为 library，也就是官方镜像。


如果想拉取指定镜像版本

```
$ docker pull ubuntu:16.04
```

### 列出镜像

```
$ docker images
```

还可以通过以下命令来便捷的查看镜像、容器、数据卷所占用的空间。

```
$ docker system df
```

### 删除本地镜像

```
$ docker image rm <镜像名> [<镜像短ID> ...]
```

比如：

```
$ docker image rm 501ad78535f0
$ docker image rm 501a
$ docker image rm centos
```

## 操作容器

有了镜像后，我们就能够以这个镜像为基础启动并运行一个容器。

### 运行容器

启动容器有两种方式，一种是基于镜像新建一个容器并启动，另外一个是将在终止状态（stopped）的容器重新启动。

1.新建并启动

```
$ docker run -it --rm -p 8888:8080 tomcat:8.0
```

2.启动和终止容器

```
$ docker ps #列出所有启动的容器
$ docker ps -a #列出所有已终止的容器
```
想要启动和终止容器，只需

```

$ docker start <容器ID>
$ docker stop <容器ID>
```

### 进入容器使用 exec 命令

docker exec 后边可以跟多个参数，这里主要说明 -i -t 参数。

只用 -i 参数时，由于没有分配伪终端，界面没有我们熟悉的 Linux 命令提示符，但命令执行结果仍然可以返回。

当 -it 参数一起使用时，则可以看到我们熟悉的 Linux 命令提示符。

```
$ docker exec -i 69d1 bash
ls
bin
boot
dev
...

$ docker exec -it 69d1 bash
root@69d137adef7a:/#
```

另外如果从这个容器中 exit，不会导致容器的停止。这就是为什么推荐大家使用 docker exec 的原因。

### 导出和导入容器

```
$ docker export 7691a814370e > ubuntu.tar
$ cat ubuntu.tar | docker import - test/ubuntu:v1.0
```

### 停用全部运行的容器

```
docker stop $(docker ps -q)
```

### 删除全部容器

```
docker rm $(docker ps -aq)
docker stop $(docker ps -q) & docker rm $(docker ps -aq) #实现一条命令停用并删除容器
```

## 常用命令
```

#同步宿主机与容器时间
$ docker run --name gaoxi-user-1 -p 18081:8080 -v /etc/localtime:/etc/localtime chaimm/tomcat:1.1

#在mac下无法使用上面的命令
$ docker run --name gaoxi-user-1 -p 18081:8080 -e TZ="Asia/Shanghai" -it chaimm/tomcat:1.1 bash

$ docker run --name zookeeper -p 2181:2181 -p 10000:8080 chaimm/zookeeper-dubbo:1.0

$ docker run --name zookeeper-1 --restart always -d zookeeper:3.4.11

#下载好的zookeeper镜像存储到本地文件
$ docker save -o /opt/downloads/zookeeper-image.tar zookeeper:3.4.11

#文件上传到内网中可以使用以下命令将其载入镜像
$docker load -i /opt/images/zookeeper-image.tar


#获取所有容器名称及其IP地址
$ docker inspect -f '{{.Name}} - {{.NetworkSettings.IPAddress }}' $(docker ps -aq) 


docker ps	顯示所有 containers
docker images	顯示所有的 images
docker rmi -f db7e8a0d84e3	移除一個 image
docker pause bb230bd64efa	停止 container 中的所有 processes
docker unpause bb230bd64efa	取消停止 container 中的所有 processes
docker logs bb230bd64efa	查看 container 的 log
docker stop bb230bd64efa	停止 container 運作
docker start bb230bd64efa	啟用 container
docker commit bb230bd64efa ubuntu:12.04	commit container 中的修改， bb230bd64efa 是 container id， ubuntu:12.04 是 image 名稱
docker run -it ubuntu:12.04 bash	啟動 container ，並登入
```

```
docker run -d --name kong\
        -e "KONG_DATABASE=postgres" \
        -e "KONG_PG_HOST=192.168.200.11" \
        -e "KONG_PROXY_ACCESS_LOG=/dev/stdout" \
        -e "KONG_ADMIN_ACCESS_LOG=/dev/stdout" \
        -e "KONG_PROXY_ERROR_LOG=/dev/stderr" \
        -e "KONG_ADMIN_ERROR_LOG=/dev/stderr" \
        -p 8888:8000 \
        -p 8445:8443 \
        -p 8889:8001 \
        -p 8446:8444 \
        kong:latest
```