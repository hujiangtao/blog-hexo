---
title: 用Hexo搭建个人博客-设置GitHub
date: 2019-12-30 20:20:30
categories:
- 用Hexo搭建个人博客
tags:
- Hexo
- github
---
静态博客可以说是从GitHub pages开始兴起的。当我们在github上配置静态博客的时候，就需要在github完成相关配置。
<!-- more -->
### 配置github pages
其实就是配置一个github的子域名指向你的静态页面配置库。Github对这个配置库的库名有一个明确的规定，需要以你的账号名为前缀连接"github.io"为库名。所以创建github pages第一步要创建一个git配置库，库名是：yourname.github.io。

然后点击进入库页面，点击标签页上的“settings”进入到设定页面还可以自定义自己的域名。

再次你要创建一个工程配置库用来管理你的博客工程，这样就不用担心数据丢失，或者在异地写博客了。