---
title: org.apache.ibatis.binding.BindingException. Parameter 'XXX'
  not found. Available parameters are [arg0, params, param1, param2]
date: 2019-07-20 22:00:13
tags:
---

## 解决方法：

导致这个错误的原因是：

```
IPage<OrderDto> page(IPage<OrderDto> page, Map<String, Object> params);
```

这里传入了多个参数，需要添加@Param注解：

```
IPage<OrderDto> page(@Param("page") IPage<OrderDto> page, @Param("params") Map<String, Object> params);
```