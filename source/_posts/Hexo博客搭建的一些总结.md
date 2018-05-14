---
title: Hexo博客搭建的一些总结
date: 2017-06-15 22:49:29
tags: hello world
categories: hello world
---
关于Hexo博客的搭建,官网提供了完善的文档，网上也能找到很多资料，这里就不再赘述了。  
### 配置GitHubSSH
1. 在gitbash中，配置github账户信息（YourName和YourEail都替换成自己的）  
2. 在gitbash中输入：```ssh-keygen -t rsa -C "youremail@example.com```，生成ssh。然后找到id_rsa.pub文件的内容  
3. 将获取的ssh放到github中，添加一个``` New SSH key ```，title随便取，key就填刚刚那一段。在gitbash中验证是否添加成功：```ssh -T git@github.com```  


### 常用hexo命令
新建文章：```hexo new "Title"```  
生成博客：```hexo g```  
发布博客：```hexo d``` 
