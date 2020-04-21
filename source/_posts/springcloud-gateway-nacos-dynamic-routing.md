---
title: springcloud-gateway-nacos-dynamic-routing
date: 2020-03-11 21:01:51
tags:
---

## nacos 发布配置

- 通过nacos提供的SDK或直接调用OPENAPI方式发布配置
- 发布配置注意多个路由放在一个配置中，而不是一个路由创建一个配置

## gateway 监听nacos下发的配置

- 使用框架提供的动态路由方法，必须使用blade-gateway-dev.json

```
[
    {
    "id": "example-list",
    "order": 0,
    "predicates": [
                {
                    "name": "Path",
                    "args": {
                        "pattern": "/api/football/match/list"
                    }
                }
            ],
            "filters": [
            ],
    "uri": "lb://ltb-api"
    },
]
```
## 