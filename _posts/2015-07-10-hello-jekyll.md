---
Date: 2015-07-10 21:33
title: Hello Jekyll
author: 老杨
layout: post
permalink: /hello-jekyll.html
categories:
  - 信息技术
tags:
  - Jekyll
---
Jekyll，你好！Github，谢谢！如果此站挂了，欢迎访问：[常阳时光(SYN) - 这是常阳时光(cyhour.com)的 Github 同步更新站.](http://syn.cyhour.com/)。

很久之前曾经试过几次用 GitHub Pages 和 Jekyll 搭建静态博客，不过因为习惯了 WordPress，又懒得动脑动手，所以一直没有折腾成功，后来就放弃了。

最近这些日子经常被 DDOS，一挂就是大半天甚至一两天，没有技术防御，更加没钱烧去防御，也不值得。所以想过直接搬到 Jekyll 或者第三方的博客平台，像 lofter……但是始终舍不得放弃 WordPress，思来想去，决定用一个不完美的解决方案——不放弃 WordPress，然后在 Github 建个镜像站（同步更新）。这样做对搜索引擎很不友好，不过，无所谓了，随缘吧。

相信 Github 肯定要比恒创靠谱好多好多好多……所以这个 Jekyll 的镜像站，除了墙的原因，应该是不会挂掉的，有待观察。

教程啥的就不说了，网上一大堆，官方也有详细的教程。Jekyll 官网：[http://jekyllrb.com](http://jekyllrb.com)，中文站：[http://jekyllcn.com](http://jekyllcn.com)。Markdown 语法说明 (简体中文版) ：[http://wowubuntu.com/markdown](http://wowubuntu.com/markdown)。

代码管理我用的是 Github 官方的 [GitHub for Windows](https://windows.github.com/)，傻瓜式，感觉用起来挺方便的。

WordPress 文章转移到 Jekyll ，我是在 WordPress 后台导出 xml，然后用 [wpXml2Jekyll 工具](https://github.com/theaob/wpXml2Jekyll)转换成单个 Markdown 文件。然后用 Sublime Text 3 批量修改文件，将 More 标签去掉。

图片还没转移，主题折腾了一下，看起来和 WordPress 这个差不多，就这样吧，先用着，慢慢完善。

更新文章都是人工同步的，评论系统也不一样，所以评论是不会同步的了，也没那能耐折腾到同步。