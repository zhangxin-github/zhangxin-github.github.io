---
title: hexo-install-theme-butterfly
date: 2020-04-23 10:15:39
tags:
---

{% tabs ,1 %}
<!-- tab 克隆最新版本 -->
在终端窗口下，定位到 butterfly 站点目录下。使用 Git checkout 代码：

{% codeblock %}
$ cd your-hexo-site
$ git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
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

当 克隆/下载 完成后，打开 **站点配置文件**， 找到 theme 字段，注释掉默认的主题并将其值更改为 butterfly。

``` bash
# theme: landscape
theme: butterfly
```