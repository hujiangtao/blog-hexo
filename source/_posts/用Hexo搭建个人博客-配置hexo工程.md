---
title: 用Hexo搭建个人博客-配置hexo工程
date: 2019-12-31 19:24:06
categories:
- 用Hexo搭建个人博客
tags:
- Hexo
---
前面说了，hexo从根本上来说是一个web程序框架；而hexo-cli脚手架提供各种快捷指令，方便我们开发配置我们需要开发的web程序。

### 安装脚手架
```
$ npm install hexo-cli -g
```
我们先通过npm全局安装hexo-cli这个给脚手架,然后就可以用hexo指令来执行一些快捷指令进行创建工程、生成页面、部署博客等等一些功能。现在我们就可以先生成一个blog工程。
```
$ hexo init blog
$ cd blog
$ npm install
```
<!-- more -->
### 将工程用git管理起来
然后在github创建一个blog配置管理库，把这个工程关联并管理起来。  
* 先进入到个人的github页面，点击Repositories右侧的New按钮，然后按照默认创建一个空的blog库：git@github.com:youname/yourblog.git
* 然后返回到本地机器，在刚刚建立的blog目录下初始化git库
    ```
    $ git init
    $ git add .                     #添加当前文件夹所有文件到暂存区
    $ git commit -m 'init blog'     #提交文件到本地库
    ```
* 将本地库与远程库关联起来
    ```
    $ git remote add origin git@github.com:youname/yourblog.git #将本地库与远程库关联起来
    $ git push -u origin master     #将本地库push到远程库中
    ```
这样就把blog工程用git管理起来了，并且可以随时把工程push github远端库里；这样可以随时在任何机器上获取你的工程文件生成博客了。
### 生成博客
现在只要运行hexo指令
```
$ hexo g
$ hexo s
```
这样我们就可以在`localhost:4000`访问初始的hexo博客了。
### 配置博客
博客的配置文件是在根目录下的`_config.yml`。需要注意的是在博客的themes目录中也有一个`_config.yml`文件；通常的我们把根目录下的`_config.yml`文件叫做**站点配置文件**，而themes目录中的`_config.yml`文件叫做**主题配置文件**  
打开站点配置文件`_config.yml`；我们需要配置的主要有这么几项。
```
# Site
title:                      # 站点标题
subtitle:                   # 站点的副标题
description:                # 站点的说明
keywords:                   # 站点的关键字
author:                     # 你的名字
language: zh-CN             # 站点语言
timezone: 'Asia/Shanghai'   # 站点的时区

url: http://www.yoursite.com #你的域名
```
上面的就是关于配置博客的一些基本信息。
然后是关于博客的部署配置，在填写配置信息之前，需要安装部署的插件
```
$ npm install hexo-deployer-git --save
```
然后修改站点配置文件`_config.yml`
```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: 'git'
  repo: git@github.com:yourname/yourname.github.io.git
  branch: master 
```
然后运行hexo治理
```
hexo d
```
或者当添加了新的日志之后运行
```
hexo clean  # 清除旧文件
hexo g      # 生成博客
hexo d      # 发布博客到github pages上
```
现在打开`https://yourname.github.io`就可看到我们的博客了。
### 写日志
运行hexo治理
```
hexo new '日志标题'
```
这样就会在source/_posts目录中生成一个`日志标题.md`的文件，然后用markdown格式编写一篇文档之后，重复以下的指令，就可以在个人博客上看到新日志了
```
hexo clean  # 清除旧文件
hexo g      # 生成博客
hexo d      # 发布博客到github pages上
```
至此，可以作为一个hexo博客的冒烟测试。
之后关于博客的标签、分类、归档以及主题的设置，将在下一篇说明。


