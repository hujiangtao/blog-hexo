---
title: 用Hexo搭建个人博客-前言
date: 2019-12-30 07:50:57
categories:
- 用Hexo搭建个人博客
tags:
- Hexo
- github
- CentOS
---

## 用Hexo搭建个人博客

### 前言
Hexo可以看作是一个静态页面生成**工程**；而不是一个博客系统。而Hexo脚手架提供了创建管理博客的命令行快捷方式，来进行创建页面、生成博客、发布博客等等。

### 规划
- 申请github page
    - 在自己的github账号下，创建一个以自己的账号名为首的以github.io为结尾的git库。然后在git库的settings中设置相关设定。
- 安装Hexo脚手架
    ```
    npm install hexo-cli -g
    ```
- 创建Hexo工程
    ````
    hexo init blog
    cd blog
    npm install
    hexo server
    ````
- 上传Hexo工程到github
    - 用git管理Hexo工程，并上传到github上，这样可以在任何地方clone hexo工程来写博客。


