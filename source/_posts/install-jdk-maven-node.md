---
title: 安装JDK-Maven-node
date: 2018-06-26 10:35:56
tags:
---


## 安装JDK
```
yum install java
```

查看安装目录
```
# ls -lrt /usr/bin/java
/usr/bin/java -> /etc/alternatives/java
# ls -lrt /etc/alternatives/java
/etc/alternatives/java -> /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.161-0.b14.el7_4.x86_64/jre/bin/java
# cd /usr/lib/jvm
# ls
java-1.8.0-openjdk-1.8.0.212.b04-0.el7_6.x86_64
jre -> /etc/alternatives/jre
jre-1.8.0 -> /etc/alternatives/jre_1.8.0
jre-1.8.0-openjdk -> /etc/alternatives/jre_1.8.0_openjdk
jre-1.8.0-openjdk-1.8.0.212.b04-0.el7_6.x86_64 -> java-1.8.0-openjdk-1.8.0.212.b04-0.el7_6.x86_64/jre
jre-openjdk -> /etc/alternatives/jre_openjdk
```

添加到PATH
```
# export JAVA_HOME=/usr/lib/jvm/jre-1.8.0-openjdk
```

## 安装maven
```
# wget http://mirror.bit.edu.cn/apache/maven/maven-3/3.6.1/binaries/apache-maven-3.6.1-bin.tar.gz
# tar xzvf apache-maven-3.6.1-bin.tar.gz
```

Adding to PATH
```
export PATH=/root/apache-maven-3.6.1/bin:$PATH
```

## 安装mysql
下载并安装MySQL官方的 Yum Repository
```
# wget -i -c http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm
# yum -y install mysql57-community-release-el7-10.noarch.rpm
# yum -y install mysql-community-server
```

首先启动MySQL
```
# sudo systemctl start mysqld.service
```

查看MySQL运行状态
```
# sudo systemctl status mysqld.service
```

但此时还有一个问题，就是因为安装了Yum Repository，以后每次yum操作都会自动更新，需要把这个卸载掉：
```
# yum -y remove mysql57-community-release-el7-10.noarch
```

查看初始密码
```
# grep "password" /var/log/mysqld.log
```

修改密码
```
ALTER USER 'root'@'localhost' IDENTIFIED BY 'z?guwrBhH7p>';
```

开放权限
```
grant all on *.* to root@'%' identified by 'z?guwrBhH7p>';
flush privileges;
```

## 安装nginx
```
# yum install nginx
# service nginx start
# service nginx stop
# service nginx restart
```

查看nginx安装目录
```
# ps -ef | grep nginx
# find /|grep nginx.conf
```