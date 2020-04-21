---
title: mysql-remote-root-user
date: 2018-08-01 20:50:08
tags:
---


# Mysql 创建用户

### 

### 使用Navicat 创建用户及分配权限

### 拷贝数据库文件

今天使用xampp的过程中， 出现mysql无法正常start的情况，通过log查看发现是table.user的索引坏了。

上网尝试了多种方法无果，只了重新安装，那么就需要把原来的库表备份出来。

在备份的过程中得知数据库引擎不同InnoDB 和MyISAM的备份方式就不同：

1. 在数据库引擎类型为InnoDB时，拷贝数据文件的同时还需要拷贝ibdata1。如果发现还是有问题，将目录下的ib_logfile*文件全部删除掉，重新启动mysql服务。
1. MyISAM类型的数据文件可以在不同操作系统中COPY，只需要拷贝数据库名字文件夹下面的文件，这样数据库就拷贝完了。