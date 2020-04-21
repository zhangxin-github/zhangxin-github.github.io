---
title: 使用Jenkins实现自动化部署
date: 2018-06-27 17:20:39
tags:
---
**Jenkins** 是一个 [持续集成](https://baike.baidu.com/item/%E6%8C%81%E7%BB%AD%E9%9B%86%E6%88%90) 工具。在这里也只是简单一用，实现下自动化部署。对于它强大的功能在日后再慢慢展开吧。

## 安装
从官网下载war包，

![jenkins download](http://7vzqnv.com1.z0.glb.clouddn.com/hexo/%5Buse-jenkins-for-auto-deploy%5DIMG_1.png)

直接放置到Tomcat目录或通过命令行 java -jar jenkins.war 运行。

## 配置

1.首次启动jenkins，出于安全考虑，jenkins会生成一个随机的口令到文件中，复制文件中的口令到jenkins即可通过访问。

![jenkins password](http://7vzqnv.com1.z0.glb.clouddn.com/hexo/use-jenkins-for-auto-deploy-WX20180701-103937.png)

2.选择安装默认插件：

![jenkins plugins](http://7vzqnv.com1.z0.glb.clouddn.com/hexo/use-jenkins-for-auto-deploy-WX20180701-104439.png)

3.跳转创建用户使用admin登录：

![jenkins account](http://7vzqnv.com1.z0.glb.clouddn.com/hexo/use-jenkins-for-auto-deploy-WX20180701-110142.png)

4.系统管理-全局工具配置-Maven、JDK安装：

![jenkins con](http://7vzqnv.com1.z0.glb.clouddn.com/hexo/use-jenkins-for-auto-deploy-WX20180701-110142.png)

## 部署SVN项目


## 常用问题

1.使用Tomcat运行jenkins时，出现安装目录在C:\Windows\System32\config\systemprofile\.jenkins\secrets\initialAdminPassword
的情况：

>因为Tomcat服务启动使用本地系统的帐户，在服务里改成具体的用户帐户即可。

![jenkins init pwd](http://7vzqnv.com1.z0.glb.clouddn.com/hexo/use-jenkins-for-auto-deploy-170630.png)

2.点击创建一个新任务，没有maven选择：

![jenkins con](http://7vzqnv.com1.z0.glb.clouddn.com/hexo/use-jenkins-for-auto-deploy-WX20180701-110406.png)

需要安装 maven integration 插件：

![maven integration](http://7vzqnv.com1.z0.glb.clouddn.com/hexo/use-jenkins-for-auto-deploy-WX20180701-112152.png)

3.如果需要发包到服务器需要安装 publish over SSH 插件:

![publish over ssh](http://7vzqnv.com1.z0.glb.clouddn.com/hexo/use-jenkins-for-auto-deploy-WX20180701-112421.png)

4.如何编译部署本地项目到服务器