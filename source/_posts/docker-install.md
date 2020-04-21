---
title: Docker安装
date: 2018-08-20 11:46:15
tags:
---

## 阿里云安装Docker

### 系统要求

Docker 运行在 CentOS 7 上，要求系统为64位、系统内核版本为 3.10 以上。

### 使用 yum 安装（CentOS 7下）

step 1: 安装必要的一些系统工具

```
sudo yum install -y yum-utils \
    device-mapper-persistent-data \
    lvm2
```

Step 2: 添加软件源信息

```
sudo yum-config-manager \
    --add-repo \
    http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

Step 3: 更新并安装Docker-CE

```
sudo yum makecache fast
sudo yum -y install docker-ce
```

Step 4: 开启Docker服务

```
sudo service docker start
```

```
# 注意：
# 安装指定版本的Docker-CE:
# Step 1: 查找Docker-CE的版本:
# yum list docker-ce.x86_64 --showduplicates | sort -r
#   Loading mirror speeds from cached hostfile
#   Loaded plugins: branch, fastestmirror, langpacks
#   docker-ce.x86_64            17.03.1.ce-1.el7.centos            docker-ce-stable
#   docker-ce.x86_64            17.03.1.ce-1.el7.centos            @docker-ce-stable
#   docker-ce.x86_64            17.03.0.ce-1.el7.centos            docker-ce-stable
#   Available Packages
# Step2: 安装指定版本的Docker-CE: (VERSION例如上面的17.03.0.ce.1-1.el7.centos)
# sudo yum -y install docker-ce-[VERSION]
```

### 使用脚本自动安装

在测试或开发环境中 Docker 官方为了简化安装流程，提供了一套便捷的安装脚本，
CentOS 系统上可以使用这套脚本安装：

```
$ curl -fsSL get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh --mirror Aliyun
```

执行这个命令后，脚本就会自动的将一切准备工作做好，并且把 Docker CE 的 Edge 版本安装在系统中。

## macOS安装Docker

### 系统要求

** Docker for Mac ** 要求系统最低为 macOS 10.10.3 Yosemite。如果系统不满足需求，可以安装 ** Docker Toolbox **。

### 手动下载安装 ###

如果需要手动安装，只需要下载 Docker for Mac。

如同 macOS 其它软件一样，安装也非常简单，双击下载的 .dmg 文件，然后将那只叫 Moby 的鲸鱼图标拖拽到 Application 文件夹即可（其间需要输入用户密码）。

## 安装校验

```
$ docker version

Client:
Version:      17.03.0-ce
API version:  1.26
Go version:   go1.7.5
Git commit:   3a232c8
Built:        Tue Feb 28 07:52:04 2017
OS/Arch:      linux/amd64
Server:
Version:      17.03.0-ce
API version:  1.26 (minimum version 1.12)
Go version:   go1.7.5
Git commit:   3a232c8
Built:        Tue Feb 28 07:52:04 2017
OS/Arch:      linux/amd64
Experimental: false
```

若能正常输出以上信息，则说明安装成功。

## 启动 Docker CE 

```
$ sudo systemctl enable docker
$ sudo systemctl start docker
```

## 删除 Docker CE

执行以下命令来删除 Docker CE：

```
$ sudo yum remove docker-ce
$ sudo rm -rf /var/lib/docker #默认安装路径
```

