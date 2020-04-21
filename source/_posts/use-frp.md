---
title: 使用frp实现内网穿透
date: 2018-07-01 00:47:43
tags:
---

** frp ** 是一个可用于内网穿透的高性能的反向代理应用，支持 tcp, udp, http, https 协议，并且支持根据域名进行路由转发。

## 开始使用

根据对应的操作系统及架构，在[Release](https://github.com/fatedier/frp/releases)页面中找到对应的frp程序。

### 外网主机

```
# 使用wget指令下载frp
wget https://github.com/fatedier/frp/releases/download/v0.13.0/frp_0.13.0_linux_amd64.tar.gz

# 使用tar指令解压tar.gz文件
tar -zxvf frp_0.13.0_linux_amd64.tar.gz

# 使用cd指令进入解压出来的文件夹，外网主机作为服务端，可以删掉不必要的客户端文件，使用rm指令删除文件。
cd frp_0.13.0_linux_amd64
rm -f frpc
rm -f frpc.ini

# 接下来要修改服务器配置文件，即frps.ini文件。使用vi指令对目标文件进行编辑。

vi frps.ini

[common]
bind_port = 7000
vhost_http_port = 80
vhost_https_port = 443

dashboard_port = 7500
dashboard_user = admin
dashboard_pwd = admin

subdomain_host = frps.com

# [common]部分是必须有的配置，其中bind_port是自己设定的frp服务端端口，vhost_http_port是自己设定的http访问端口, dashboard_port是控制台端口， subdomain_host自定义域名路由。

# 保存上面的配置后，使用以下指令启动frp服务端。（如果需要在后台运行，请往下翻阅关于后台运行的部分。）

# 服务端的工作就到此结束了。
./frps -c ./frps.ini
```

### 客户端

客户端前面的操作和服务端一样，根据自己的操作系统下载对应的程序，这里不一一解释。主要看下客户端的配置：

```
[common]
server_addr = x.x.x.x
server_port = 7000

[web]
type = http
local_port = 80
custom_domains = no2.sunnyrx.com
```

上面的配置和服务端是对应的。

[common]中的server_addr填frp服务端的ip（也就是外网主机的IP），server_port填frp服务端的bind_prot。

[web]同上，local_port填群晖的web端口。这里创建了两个http反向代理是为了分别映射群晖两个重要的端口，5000和80，前者用于登录群晖管理，后者用于群晖的Web Station和DS Photo。

保存配置，输入以下指令运行frp客户端。（同样如果需要在后台运行，请往下翻阅关于后台运行的部分。）

```
./frpc -c ./frpc.ini
```

此时在服务端会看到”start proxy sucess”字样，即连接成功。

### 让frp在后台运行

虽然现在frp运作起来了，内网穿透也实现了，但这还是不够的。此时如果断开与服务端或者客户端的SSH连接（比如关掉了Xshell）也就中止了frp的运行。

保持frp运行是关键是让服务端的frp和客户端的frp在后台运行，这里提两个方法供参考，一个是使用supervisor，另一个是使用winsw, 分别实现了linux和windows下后台运行。

1. supervisor

```
# 需要知道几个名词
supervisor：要安装的软件的名称。 
supervisord：装好supervisor软件后，supervisord用于启动supervisor服务。 
supervisorctl：用于管理supervisor配置文件中program。
```

```
# 安装
yum install supervisor

# 开机自启动
systemctl enable supervisord 

# 查看是否启动
systemctl is-enabled supervisord

# 启动supervisord服务
systemctl start supervisord 

# 查看supervisord服务状态
systemctl status supervisord 

# 查看是否存在supervisord进程
ps -ef|grep supervisord 

# 停止
systemctl stop supervisord

# 重启
systemctl restart supervisord
```

默认安装supervisor文件会生成在下面的路径中：

```
/etc/supervisord.conf
/etc/supervisord.d/
```

然后在/etc/supervisor.d下新建一个配置文件frps.ini，输入以下内容。command应该是你放置frps软件的位置。

```
[program:frps]
command = /opt/frp/frp_0.9.3_linux_amd64/frps -c /opt/frp/frp_0.9.3_linux_amd64/frps.ini
autostart = true
```

然后使用上面的命令启动supervisor。

2.winsw

[winsw](https://github.com/kohsuke/winsw/releases)能让Windows程序运行为服务，只需要将winsw.exe和frpc.exe放到了一起，这样只需要直接填写程序名称。然后在和winsw.exe同级的目录下，新建winsw.xml文件，输入以下内容。

```
<service>
    <id>frp</id>
    <name>frp</name>
    <description>用frp发布本地电脑网站到外网</description>
    <executable>frpc</executable>
    <arguments>-c frpc.ini</arguments>
    <logmode>reset</logmode>
</service>
```

然后打开管理员权限命令提示符，使用下面的命令安装并启动服务。

```
winsw install
winsw uninstall
```