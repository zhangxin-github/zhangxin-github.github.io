---
title: 使用VuePress生成项目文档网站
date: 2018-09-23 16:33:02
tags:
---

**VuePress** 是一个基于Vue的轻量级静态网站生成器，用于满足项目文档的需求而创建的。

## VuePress 安装

VuePress并不会象其他静态网站工具如：Hexo 那样帮我们创建好目录结构和文件。因此需要我们在指定文件夹中新建目录结构和文件如下：

```
.
├─ docs
│  └─ .vuepress
│     └─ config.js
│  ├─ guide
│     └─ getting-started.md
│     └─ README.md
│  ├─ README.md
└─ package.json
```

###  config.js

网站的 [配置]() 信息，您可以在此配置大部分的参数。这里提供常用基本的配置：

```
module.exports = {
    base:'/vuepress/',
    title: 'Wizard',
    description: 'Welcome to Wizard site',
    themeConfig: {
        nav: [
            { text: 'Home', link: '/' },
            { text: '指南', link: '/guide/' },
            { text: 'VuePress', link: 'https://vuepress.vuejs.org/' },
        ],
        sidebar: { '/guide/': genSidebarConfig('指南') }
    }
}

function genSidebarConfig(title) {
    return [
        {
          title,
          collapsable: false,
          children: [
            '',
            'getting-started',
          ]
        }
      ]
}
```

### package.json

应用程序的信息。

```
{
  "scripts": {
    "docs:dev": "vuepress dev docs",
    "docs:build": "vuepress build docs",
    "deploy": "gh-pages -d docs/.vuepress/dist",
    "deploy:build": "npm run docs:build && gh-pages -d docs/.vuepress/dist"
  },
  "devDependencies": {
    "gh-pages": "^2.0.0"
  }
}
```

### 指令

执行下列命令，可以开始写作了。

```
# 全局安装VuePress
npm install -g vuepress

# 安装组件
npm install

# 开始写作
npm run docs:dev

# 构建静态文件
npm run docs:build
```

### 在Github Page部署

1. 创建仓库

> - 如果要部署到https://{USERNAME}.github.io地址上，需要创建以{USERNAME}.github.io为名字的仓库
> - 如果部署到https://{USERNAME}.github.io/{REPO}/地址上，要创建{REPO}仓库。

2. 添加远程仓库

```
# 用你仓库的url
git remote add origin https://<USERNAME>.github.io/<REPO>.git   

# 提交到你的仓库
git push -u origin master  
```

3. 发布

```
# 使用gh-pages组件打包并推送
$ sudo npm run deploy:build
```
看到如下日志部署成功：

```
> npm run docs:build && gh-pages -d docs/.vuepress/dist

> vuepress build docs

 WAIT  Extracting site metadata...
[13:51:40] Compiling Client
[13:51:40] Compiling Server
(node:2939) DeprecationWarning: Tapable.plugin is deprecated. Use new API on `.hooks` instead
[13:51:45] Compiled Server in 5s
[13:51:49] Compiled Client in 9s
 WAIT  Rendering static HTML...

 DONE  Success! Generated static files in docs/.vuepress/dist.

Published
```

部署成功后，进入 GitHub 仓库可以看到自动创建了一个新的名为 gh_pages 的分支。在仓库 **setting** 中选择这个分支，通过如下地址即可访问：

https://{USERNAME}.github.io/{REPO}

