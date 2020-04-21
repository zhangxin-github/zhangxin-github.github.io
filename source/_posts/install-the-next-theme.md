---
title: 安装NexT主题
date: 2018-06-26 10:35:56
tags:
---
Hexo 安装主题的方式非常简单，只需要将主题文件拷贝至站点目录的 themes 目录下， 然后修改下配置文件即可。

### 下载主题包

{% tabs ,1 %}
<!-- tab 克隆最新版本 -->
在终端窗口下，定位到 Hexo 站点目录下。使用 Git checkout 代码：

{% codeblock %}
$ cd your-hexo-site
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
{% endcodeblock %}

<!-- endtab -->
<!-- tab 下载稳定版本 -->
前往 NexT 版本 [发布页面](https://github.com/iissnan/hexo-theme-next/releases)。
选择你所需要的版本，下载 Download 区域下的 Source Code (zip) 到本地。例如，下载 v0.4.0 版本： 
![next-releases](https://theme-next.iissnan.com/uploads/five-minutes-setup/download-stable-version.png)
解压所下载的压缩包至站点的 themes 目录下， 并将 解压后的文件夹名称（hexo-theme-next-0.4.0）更改为 next。
<!-- endtab -->
{% endtabs %}

### 启用主题

当 克隆/下载 完成后，打开 **站点配置文件**， 找到 theme 字段，注释掉默认的主题并将其值更改为 next。

``` bash
# theme: landscape
theme: next
```

启动 Hexo 本地站点，并开启调试模式（即加上 --debug），整个命令是 

``` bash
hexo s --debug。 
```

### 选择 Scheme

NexT 提供三种不同风格主题方案：
![NexT-Schemes](https://theme-next.iissnan.com/assets/img/NextSchemes3.png)
Scheme 的切换通过更改 **主题配置文件**，搜索 scheme 关键字。 你会看到有三行 scheme 的配置，将你需用启用的 scheme 前面注释 # 去除即可。

``` bash
#scheme: Muse
#scheme: Mist
#scheme: Pisces
scheme: Gemini
```


