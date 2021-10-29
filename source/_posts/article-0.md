---
title: Hello World
date: 2019-09-01 19:26:44
comments: true
tags:
- Hexo
- Github Page
categories: 日常流水账
---
学习Github Page +Hexo 搭建博客
<!--more-->
之前debu推荐Gridea +Github Page的方式搭建blog，但是在Gridea远程连接的时候失败了。今天心血来潮，决定尝试一下Hexo。

## Hexo +Github Page

记录一下我用到的教程和遇到的问题及解决办法：

[【不定期更新】最新从零开始Github Pages +Hexo 搭建个人静态博客与Next主题个性化配置/up主：Moveeeeee](https://www.bilibili.com/video/av36938592/?p=1)

[Moveeeeee的blog](https://www.lixint.me/hexo-blog.html)

这个教程非常详细，完全适合我这种小白操作，教程里面hexo的版本是1.1.0，现在安装的hexo是2.0。教程中配置完SSH Key后，修改Hexo站点配置文件，然后hexo g生成页面，hexo d上传至Github。但hexo d时会出现一个类似于找不到global user name的问题。其实是少了一步配置。查了[另一个教程](https://www.cnblogs.com/liuxianan/p/build-blog-website-by-hexo-github.html)，误打误撞找到了解决办法：

>$ git config --global user.name "liuxianan"// 你的github用户名，非昵称
>$ git config --global user.email  "xxx@qq.com"// 填写你的github注册邮箱

进行完这一步，再hexo g -d就搭建成功了。hexo s可以本地预览改改错别字（

## Hexo主题

Hexo官网上有很多好看的主题，选择比Gridea多一些，部分主题支持移动设备。

我用了[Ocean](https://zhwangart.github.io/)这个主题，简单学习了一下如何修改主题，还没有学会（x

其他功能以后用的时候再说吧（等等党的胜利（

现在尝试发布第一篇blog，顺便学习了一下markdown语言。虽然之前用Bear也支持markdown，但是傻瓜操作，不需要记语言。赞美Bear（（
