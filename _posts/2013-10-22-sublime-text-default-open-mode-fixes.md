---
title: Sublime Text 默认打开方式修复
author: 老杨
layout: post
permalink: /sublime-text-default-open-mode-fixes.html
categories:
  - 信息技术
tags:
  - Sublime Text
---
因为wordpress，用上了 Sublime Text 2，很好用，但是有个非常明显的缺点——启动速度奇慢。

zww大叔说 Sublime Text 3 基本上是秒开，于是网上找了个xx版，顺利安装完，xx了——确实秒开。

但是，卸载了 Sublime Text 2 ，问题来了——无法将php等文件默认打开方式设置为Sublime Text 3。

<span style="color: #ff0000;">网上找来的解决办法：</span>regedit打开注册表，然后搜索Sublime\_Text.exe，将 HKEY\_CLASSES\_ROOTApplicationssublime\_text.exeshellopencommand 默认键值设置为E:SoftWareSublime Text 3sublime_text.exe "%1" （地址改为你sublime text的文件地址）

![sublime_text3][1]

然后，右键就可以设置默认打开方式了。

 [1]: http://cyhour.com/wp-content/uploads/2013/11/sublime_text3.jpg