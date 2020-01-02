---
title: 用Hexo搭建个人博客-配置主题
date: 2020-01-01 19:43:42
categories:
- 用Hexo搭建个人博客
tags:
- Hexo
---
谁都喜欢赏心悦目的东西，但是一般人却未必由美术的功底。为了让自己的博客好看一些，使用现成的主题就是一个很好的选择了。Next主题到现在以及是v7.6.0了，可以看出它有稳定的团队，而且经过这么长时间的迭代，版本的bug必然会少一些。

### 下载Next
因为我选择把博客工程用git管理起来，为了方式git的版本嵌套问题。我没有把Next主题在工程内部clone，而是在工程外选择一个文件夹clone Next工程。
```
$ cd ~/
$ mkdir themes
$ cd themes
$ git clone https://github.com/theme-next/hexo-theme-next
```
把Next主题clone下之后，拷贝到我们的博客工程中，先在博客工程的themes目录下建立一个next目录，然后copy Next主题的文件到这个目录
<!-- more -->
```
$ cd ~/blog/themes
$ mkdir next
$ cp ~/themes/hexo-thems-next/* -Rf ./next 
```
### 配置站点主题
先打开博客工程的根目录下的站点配置文件`_config.yml`；
```
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: next                             #添加这个配置项
```
运行hexo指令
```
hexo s
```
打开https://localhost:4000/ 我们就可以看到主题模式已经改成了Next主题了。

### 配置Next主题。
在Next主题还有一些配置项，可以让主题更适合你的审美。
#### 设置主页连接菜单
```
menu:
  home: / || home
  tags: /tags/ || tags
  categories: /categories/ || th
  archives: /archives/ || archive
  about: /about/ || user
  #schedule: /schedule/ || calendar
  #sitemap: /sitemap.xml || sitemap
  #commonweal: /404/ || heartbeat
```
在这里按照需要，就可以添加相关的链接；在添加完链接后，还需要添加相关的页面。比如上面的例子，还需要添加tags页面、categories页面以及about页面。
* **添加tags页面**
```
$ hexo new page "tags"
```
然后在source目录下就可以看到增加了一个tags目录，目录中添加了一个 index.md；打开index.md 文件。我们添加一个Front-matter项
```
---
title: 标签
date: 2019-12-29 08:36:37
type: "tags"                # 添加项
---
```
这样我们在文章中添加了tags就可以自动在tags页面显示了，categories也一样。
* **添加categories**
```
$ hexo new page "categories"
```
然后打开 source/categories/index.md
```
---
title: 分类
date: 2019-12-29 08:37:56
type: "categories"          # 添加项
---
```
#### 设置Scheme
```
# ---------------------------------------------------------------
# Scheme Settings
# ---------------------------------------------------------------

# Schemes
#scheme: Muse
#scheme: Mist
#scheme: Pisces
scheme: Gemini      #去掉注释，现在这个scheme
```
Next主题有几个不同的Scheme，你可以选择一个你喜欢的去掉注释，然后把其他的注释起来就可以了。

#### 设置字体
在这里我们可以设置字体大小和字体样式，首先要打开配置项，将enable设置为true，然后按照提示设置相应的设置就可以了，我这里之更改了字体的大小。将字体从16px改成了14px，然后把主题也等比例缩小了
```
font:
  enable: true      #打开配置

  # Uri of fonts host, e.g. //fonts.googleapis.com (Default).
  host:

  # Font options:
  # `external: true` will load this font family from `host` above.
  # `family: Times New Roman`. Without any quotes.
  # `size: x.x`. Use `em` as unit. Default: 1 (16px)

  # Global font settings used for all elements inside <body>.
  global:
    external: true
    family: Lato
    size: 0.875         #默认是1，就是16px，这里选择14px，就是0.875em

  # Font settings for site title (.site-title).
  title:
    external: true
    family:
    size: 

  # Font settings for headlines (<h1> to <h6>).
  headings:
    external: true
    family:
    size: 1.42          #在base配置文件中是1.625em，这里等比例缩小之1.42em
```

在主题配置文件中，还有很多配置项。设置还有很多插件我都没有涉及，这里只是保证博客最低可以运行的配置，其他的提高设置等到以后有时间再总结。hexo的初步使用就到此为止。