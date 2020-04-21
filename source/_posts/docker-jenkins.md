---
title: 在Docker中运行Jenkins
date: 2018-08-23 11:46:07
tags:
---

## 拉取jenkins镜像 ##

```
docker pull jenkins
```

## 创建jenkins容器 ##

```
docker run -p 18080:8080 -p 50000:50000 -v /usr/maven/apache-maven-3.5.3:/Users/xinzhang/Downloads/apache-maven-3.5.3 jenkins
```