---
title: IntelliJ IDEA 使用
date: 2019-07-28 23:25:41
tags:
---

## 下载安装

## 快捷方式

## 常用插件

## FAQ

### 1.无法启动

```
打开finder->应用程序->idea.app->右键->显示包内容->然后MaxOS->双击shell脚本（idea）
```
这样是通过命令行的方式来启动IDEA。
仔细看里面的提示，尤其Error开头的信息，应该会有具体原因。

you know？ 然后JetbrainsCrack-3.1-release-enc.jar 被我不小心删了，放回原位就好了......


### 1.永久使用

在输入验证码时，一直提示“key is invaild”，打开~/资源库/Preferences/
其中有个 IntelliJIdea2018.2 文件，里面也会有个idea.vmoptions ，也在最后一行加入；

```
-javaagent:JetbrainsCrack-3.1-release-enc.jar
```

再打开软件再次输入验证码即可：

```
{"licenseId":"1337",
"licenseeName":"ChaosGod",
"assigneeName":"",
"assigneeEmail":"",
"licenseRestriction":"Unlimited license till end of the century.",
"checkConcurrentUse":false,
"products":[
{"code":"II","paidUpTo":"2099-12-31"},
{"code":"DM","paidUpTo":"2099-12-31"},
{"code":"AC","paidUpTo":"2099-12-31"},
{"code":"RS0","paidUpTo":"2099-12-31"},
{"code":"WS","paidUpTo":"2099-12-31"},
{"code":"DPN","paidUpTo":"2099-12-31"},
{"code":"RC","paidUpTo":"2099-12-31"},
{"code":"PS","paidUpTo":"2099-12-31"},
{"code":"DC","paidUpTo":"2099-12-31"},
{"code":"RM","paidUpTo":"2099-12-31"},
{"code":"CL","paidUpTo":"2099-12-31"},
{"code":"PC","paidUpTo":"2099-12-31"},
{"code":"DB","paidUpTo":"2099-12-31"},
{"code":"GO","paidUpTo":"2099-12-31"},
{"code":"RD","paidUpTo":"2099-12-31"}
],
"hash":"2911276/0",
"gracePeriodDays":7,
"autoProlongated":false}
```