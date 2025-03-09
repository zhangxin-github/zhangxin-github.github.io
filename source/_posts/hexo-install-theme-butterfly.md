---
title: hexo-install-theme-butterfly
date: 2020-04-23 10:15:39
tags:
top_img: /images/hexo-install-theme-butterfly/butterfly-docs-03-cover.png # 顶部背景图
cover: /images/hexo-install-theme-butterfly/butterfly-docs-03-cover.png   # 文章封面
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

### 导航菜单 
1. 在站点配置文件 **_config.yml** 中，找到 menu 字段，并添加以下内容：

```js
menu:
  Home: / || fas fa-home
  归档: /archives/ || fas fa-archive
  标签: /tags/ || fas fa-tags
  分类: /categories/ || fas fa-folder-open
  娱乐||fas fa-list:
    音乐: /music/ || fas fa-music
    照片: /photo/ || fa-solid fa-image
    电影: /movies/ || fas fa-video
  友链: /link/ || fas fa-link
  闲言: /write/ || fa-solid fa-feather-pointed
  留言: /talk2me/ || fas fa-comment-dots
  关于: /about/ || fas fa-heart
```

### 本地搜索
1. 安装插件：
```shell
$ npm install hexo-generator-search --save
```

2. 修改配置文件 **_config.yml**：
```yaml
search:
  # Choose: algolia_search / local_search / docsearch
  use: local_search
```

### 创建文件夹
```shell
$ hexo new page "archives"
$ hexo new page "tags"
$ hexo new page "categories"
```

### 修改副标题
```shell
subtitle:
  enable: true
  # Choose: false/1/2/3
  # false - disable the function
  # 1 - hitokoto.cn
  # 2 - https://api.aa1.cn/doc/yiyan.html
  # 3 - jinrishici.com
  source: 2
```
### 字数统计
```shell
# Need to install the hexo-wordcount plugin
npm install hexo-wordcount --save

# Configuration
wordcount:
  enable: true
  post_wordcount: true
  min2read: true
  total_wordcount: true
```

### 图片设置

1. 主页封面图片
   
```yaml
index_img: /img/index.jpg
```

1. footer 背景
```yaml
# footer是否显示图片背景(与top_img一致)
footer_img: true
```

2. 文章详情页图片

```yaml
---
title: Hello World        # 标题
tags: [hello]             # 标签
categories:               # 分类
description: hello word~  # 描述
top_img: /images/hexo-install-theme-butterfly/butterfly-docs-03-cover.png # 文章顶部背景图
cover: /images/hexo-install-theme-butterfly/butterfly-docs-03-cover.png   # 文章封面
---
```

3. 归档顶部图片

```yaml
archive_img: /img/archive.jpg
```


4. 标签顶部图片

```yaml
tag_img: /img/tag.jpg
```

4. 分类顶部图片

```yaml
category_img: /img/category.jpg
```
