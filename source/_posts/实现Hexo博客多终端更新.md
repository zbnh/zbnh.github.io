---
title: 实现Hexo博客多终端更新
date: 2018-05-17 09:06:47
tags: [hello world,hexo,多终端更新,git]
categories: hello world
---
搭建完hexo博客后遇到的一个问题就是多终端更新，我们经常需要在自己的电脑或单位的电脑上更新博客，这需要一些操作，巧妙地使用git和branch即可实现多终端更新。  
# 原理
利用git的分支（branch）管理功能，hexo博客源文件放在hexo分支上，编译出来的html文件放在master分支上，以此实现多终端更新和同步。
<!-- more -->
# 操作方法
网上关于hexo多终端更新的文章很多，基本原理大体一致，可以参考简书上的这篇文章[Hexo博客的跨设备同步](https://www.jianshu.com/p/6fb0b287f950)。接下来说一下容易遇到的问题。
# 疑难问题
* ## 编译后页面空白
1. 原因  
这是因为主题theme文件夹下缺失第三方主题文件造成的，如果使用了第三方主题，第三方主题的文件夹大多是git repository，hexo源文件根目录在git init时会忽略已有的repository。  
2. 解决方法  
从原来电脑上把主题文件手动复制过来或使用git submodule功能（详见[Git 工具 - 子模块](https://git-scm.com/book/zh/v1/Git-工具-子模块)）。  
* ## 报错Error: Host key verification failed.  
这是因为未配置SSH Key，关于配置SSH Public Key，详情参考这篇文章[hexo git配置问题笔记](https://www.cnblogs.com/imsoft/p/5228560.html)