---
title: 更新 Show UserAgent IP 库
author: 大肥羊
layout: post
permalink: /show-useragent-ip-library-update.html
categories:
  - 信息技术
tags:
  - Show UserAgent
  - 评论者国旗
---
<a href="https://wordpress.org/plugins/show-useragent/" target="_blank">Show UserAgent</a>：用于显示访客UA信息的插件，包括：操作系统信息，浏览器信息以及国籍信息（显示评论者所在地国旗）。作者：<a href="http://hzlzh.io/show-useragent/" target="_blank" rel="nofollow">hzlzh</a>。插件的 IP 库最后更新时间是 2012.08.25，已经两年多没更新了，好些 IP 不能正确显示国旗了，搜了搜资料，更新了一下 IP 库，需要的直接下载替换文件即可。  


  
数据取自 <a href="http://software77.net/geo-ip/" target="_blank" rel="nofollow">Software77.net</a> 最新（2015-1-25） IPV4 库，度娘网盘下载地址：http://pan.baidu.com/s/1ntC7eOT

附上 CSV 格式 IP 库转换成插件支持的 bin 格式简单方法（Windows）：

  1. 安装 <a href="https://www.java.com" target="_blank" rel="nofollow">java</a>；
  2. 到 <a href="http://software77.net/geo-ip/" target="_blank" rel="nofollow">Software77.net</a> 下载最新的 IPV4 库的 csv 文件；
  3. 下载转换工具：http://pan.baidu.com/s/1c0hburY
  4. 将转换工具和 IPV4 库的 csv 文件放至同一文件夹内，如：<a href="http://firestats.cc/wiki/ip2c" target="_blank">ip2c</a>；
  5. 进入 ip2c 文件夹，运行命令：<span style = "color:red;">java -jar ip2c.jar -c ip-to-country.csv</span> ，如不能正常编译，将 ip2c.jar 文件添加到 Windows 的环境变量路径去（Build Path）。

转换截图：

![ ip2c-build ][1]

 [1]: https://cyhour.com/wp-content/uploads/2015/01/ip2c-build.png