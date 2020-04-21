---
title: If you are using vue-loader@>=10.0, simply update vue-template-compiler
date: 2019-09-12 15:57:33
tags:
---

## 问题说明

```
Module build failed: Error: 

Vue packages version mismatch:

- vue@2.5.17 (/Users/xinzhang/Documents/IdeaProjects/incubator-vue-antd-admin/node_modules/vue/dist/vue.runtime.common.js)
- vue-template-compiler@2.6.10 (/Users/xinzhang/Documents/IdeaProjects/incubator-vue-antd-admin/node_modules/vue-template-compiler/package.json)

This may cause things to work incorrectly. Make sure to use the same version for both.
If you are using vue-loader@>=10.0, simply update vue-template-compiler.
If you are using vue-loader@<10.0 or vueify, re-installing vue-loader/vueify should bump vue-template-compiler to the latest.
```

## 解决方法

经常有启动vue工程时会出现如上错误提示，出现这种错误之后可以使用命令，将vue的版本改成和vue-template-compiler的版本一致，使用命令

```
npm install vue@2.6.10 --save 
yarn add vue@2.6.10
```
