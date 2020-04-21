---
title: spingboot静态资源路径
date: 2019-09-26 18:01:08
tags:
---

Spring Boot 默认提供了静态资源处理，而有时我们需要自定义资源映射，可定义项目内部目录，也可定义外部目录。

## 通过文件配置

```xml
spring:
    mvc:
        static-path-pattern: /**
    resources:
         static-locations: classpath:/META-INF/resources/,classpath:/resources/, classpath:/static/, classpath:/public/
```

上面这几个都是静态资源的映射路径，优先级顺序为：META-INF/resources > resources > static > public
如果你想指定外部的目录也很简单，直接addResourceLocations指定即可，代码如下：

```
spring:
    mvc:
        static-path-pattern: /**
    resources:
        static-locations: classpath:/META-INF/resources/,classpath:/resources/, classpath:/static/, classpath:/public/, file:${uploadfile}

uploadfile: /home/upload/
```

## 通过@Configuration配置

```
@Configuration
public class ApplicationConfig extends WebMvcConfigurerAdapter {

    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/**")
                .addResourceLocations("classpath:/META-INF/resources/")
                .addResourceLocations("classpath:/resources/")
                .addResourceLocations("classpath:/static/")
                .addResourceLocations("classpath:/public/");
        registry.addResourceHandler("/upload/**").addResourceLocations("file:/home/upload/");
        super.addResourceHandlers(registry);
    }
}
```

### 注意

1. 无论文件配置方式还是注解方式，一定要注意路径最后的“/”必须要有。
1. 通过注解方式配置会覆盖默认配置。