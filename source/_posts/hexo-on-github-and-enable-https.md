---
title: 利用GitHub搭建Hexo博客并开启HTTPS
---
**Hexo** 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
**GitHub** 是一个面向开源及私有软件项目的托管平台, 它提供的 **GitHub Pages** 是一个静态站点托管服务，旨在直接从GitHub存储库托管个人、组织或项目页面。

## 安装Hexo

### 安装前提

安装 Hexo 相当简单。然而在安装前，先检查是否已安装下列应用程序：

- Node.js
- Git

如果您的电脑中已经安装上述必备程序，那么只需要使用 npm 即可完成 Hexo 的安装。

``` bash
$ npm install -g hexo-cli
```

安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。

``` bash
$ hexo init <folder>
$ cd <folder>
$ npm install （貌似不需要这步，执行init就会install了）
```

新建完成后，指定文件夹的目录如下：

``` bash
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

## 开始

### 写文章

``` bash
$ hexo new "My New Post"
```

如果没有设置 layout 的话，默认使用 _config.yml 中的 default_layout 参数代替。如果标题包含空格的话，请使用引号括起来。

### 本地运行服务

``` bash
$ hexo server
```

### 本地运行清除缓存

``` bash
$ hexo clean
```

在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。

### 部署

``` bash
$ hexo publish "My New Post"
$ hexo generate --deploy
```

> - $ hexo publish 发表草稿
> - $ hexo g -d 文件生成后立即部署网站

** 如果使用Git服务存放，在执行部署前需要先安装 hexo-deployer-git **

``` bash
$ npm install hexo-deployer-git --save
```

修改网站根目录下的_config.yml配置:

``` bash
deploy:
  type: git
  repo: <repository url>
  branch: [branch]
``` 

| 参数	|  描述 | 
| :--------  | :-----  |
| repo | 库（Repository）地址 | 
| branch | 	分支名称 | 

## 自定义域名

### 域名解析

开启 Github Pages，创建一个命名为：username.github.io 的资源库，这里的username就是你的用户名。如果想使用自定义域名需要在域名解析管理新增 CNAME 解析：

| 记录类型    | 主机记录   |  记录值  |
| :--------:  | :-----:  | :----:  |
| CNAME     |   @     | username.github.io    |
| CNAME     |   www   | username.github.io    |

### GitHub Pages 配置

完成域名解析后还需要在 GitHub Pages 仓库根目录下创建CNAME文件，文件内容为自定义的域名，例如：hellozhang.xin

### GitHub Pages 开启HTTPS：

- 在 GitHub Pages 存储库的主页面下，单击设置。

![Repository settings button](https://help.github.com/assets/images/help/repository/repo-actions-settings.png)

- 在“GitHub页面”下，选择强制HTTPS。

![Enforce HTTPS checkbox](https://help.github.com/assets/images/help/pages/enforce-https-checkbox.png)

> 如果使用Chrome浏览器未能在地址栏出现 **绿色小锁** 或出现小叹号提示网站与建立完全安全的链接，请检查自己的网站引用的资源文件有没有使用了 http 协议，请替换成相应的 https 资源。可通过F12开发者工具检查。

| Asset type	    | HTTP   |  HTTPS  |
| :--------:  | :-----:  | :----:  |
| CSS | <link rel=”stylesheet” href=”http://example.com/css/main.css"> | <link rel=”stylesheet” href=”https://example.com/css/main.css"> |
| JavaScript | <script type=”text/javascript” src=”http://example.com/js/main.js"></script>	| <script type=”text/javascript” src=”https://example.com/js/main.js"></script> |
| Image |  <A HREF=”http://www.somesite.com"><IMG SRC=”http://www.example.com/logo.jpg" alt=”Logo”></a>	| <A HREF=”https://www.somesite.com"><IMG SRC=”https://www.example.com/logo.jpg" alt=”Logo”></a> |