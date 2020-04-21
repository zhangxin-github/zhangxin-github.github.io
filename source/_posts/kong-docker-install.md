---
title: kong使用docker安装
date: 2018-08-30 16:04:42
tags:
---

## Kong

Kong 是在客户端和（微）服务间转发API通信的API网关。 Kong 可以通过插件扩展已有功能，这些插件在 API 请求响应循环的生命周期中被执行。插件使用 Lua 编写，而且 Kong 还有如下几个基础功能：HTTP 基本认证、密钥认证、CORS（ Cross-origin Resource Sharing，跨域资源共享）、TCP、UDP、文件日志、API 请求限流、请求转发以及 nginx 监控。

## 根据官网提供的脚本和步骤进行安装

1.创建一个自定义网络，允许容器发现并相互通信。在这个例子中，kong-net是网络名称，可以使用任何名称:

```
docker network create kong-net
```

2.如果希望使用 PostgreSQL 容器：

```
docker run -d --name kong-database \
    --network=kong-net \
    -p 15432:5432 \
    -e "POSTGRES_USER=kong" \
    -e "POSTGRES_DB=kong" \
    -v /etc/localtime:/etc/localtime:ro \ # 同步宿主机时间
    postgres:9.6
```

3.准备数据库:

```
docker run --rm \
    --network=kong-net \
    -e "KONG_DATABASE=postgres" \
    -e "KONG_PG_HOST=kong-database" \
    -e "KONG_CASSANDRA_CONTACT_POINTS=kong-database" \
    kong kong migrations up
```

4.启动一个连接数据库容器的kong容器:

```
docker run -d --name kong \
    --network=kong-net \
    -e "KONG_DATABASE=postgres" \
    -e "KONG_PG_HOST=kong-database" \
    -e "KONG_CASSANDRA_CONTACT_POINTS=kong-database" \
    -e "KONG_PROXY_ACCESS_LOG=/dev/stdout" \
    -e "KONG_ADMIN_ACCESS_LOG=/dev/stdout" \
    -e "KONG_PROXY_ERROR_LOG=/dev/stderr" \
    -e "KONG_ADMIN_ERROR_LOG=/dev/stderr" \
    -e "KONG_ADMIN_LISTEN=0.0.0.0:8001, 0.0.0.0:8444 ssl" \
    -v /etc/localtime:/etc/localtime:ro \ # 同步宿主机时间
    -p 18000:8000 \
    -p 18443:8443 \
    -p 18001:8001 \
    -p 18444:8444 \
    kong
```

如果出现：

```
Error: could not prepare Kong prefix at /usr/local/kong: nginx configuration is invalid (exit code 1):
nginx: the configuration file /usr/local/kong/nginx.conf syntax is ok
nginx: [alert] mmap(MAP_ANON|MAP_SHARED, 134217728) failed (12: Out of memory)
nginx: configuration file /usr/local/kong/nginx.conf test failed
```

则使用：

```
sudo docker run -d --name kong \
    ...
```


测试

```
$ curl -i http://localhost:8001/
```

### kong-dashboard 要配合 kong 的版本，因此上面kong使用0.13版本

```
$ docker run --rm -p 8080:8080 pgbi/kong-dashboard start --kong-url http://kong-ip:8001
```

### pg管理后台
docker run -p 10080:80 \
--link kong-database:kong-database \
-e "PGADMIN_DEFAULT_EMAIL=user@domain.com" \
-e "PGADMIN_DEFAULT_PASSWORD=SuperSecret" \
-d dpage/pgadmin4