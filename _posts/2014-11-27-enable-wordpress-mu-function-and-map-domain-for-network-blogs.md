---
title: 折腾WordPress MU多站点设置与独立域名映射
author: 大肥羊
layout: post
permalink: /enable-wordpress-mu-function-and-map-domain-for-network-blogs.html
categories:
  - 信息技术
tags:
  - 多站点博客
---
在WordPress 3.0版本中，已经开始提供了创建一个多站点博客网络的功能，此文仅是记录一下折腾如何创建这么一个网络的说明。<span style = "color:red;">切记，开启多站点博客网络之前一定要先备份好数据。</span>  


  
基本流程：检查主机是否支持 –> 全新安装 WordPress 3.0+ –> 启用 Network –> 导入数据 –> 调整数据 –> 独立域名映射。

### 检查主机是否支持

WordPress 必须安装在网站根目录下，创建网络时会让您选择是以<span style = "color:red;">子域名</span>的方式来创建网络，还是以<span style = "color:blue;">子目录</span>的方式来创建网络，它们的形式如下：

  * 子域名方式 —— site1.example.com 或 site2.example.com，原理是使用通配符子域（即'*'），必须在Apache中开启此功能, 然后在DNS记录里添加通配符子域。有些主机已经设置了通配符在服务器端,这意味着您只需要添加DNS记录。 一些共享的主机商可能不支持这个，所以您可能需要启用此功能前，请检查您的虚拟主机提供商。
  * 子目录方式 —— example.com/site1 或 example.com/site2，原理是使用服务器上 <a href="http://codex.wordpress.org/Glossary#mod_rewrite" target="_blank">mod_rewrite</a> 的功能，需有阅读 .htaccess 文档的基础知识。

### WordPress 必要的设置

  1. 如下列的情况,那你不能创建一个站点网络 :
  * "WordPress地址 (URL)" 不等同于 "网站地址(URL)".
  * "WordPress地址(URL)" 使用数字端口':80', ':443'.

  2. 如下列的情况,你不能选择 子域 安装:
  * WordPress安装在一个目录（文件夹）里（不是根目录）.
  * "WordPress地址(URL)" 是localhost（即本地环境）.
  * "WordPress地址(URL)" 是IP地址,如127.0.0.1.

### 安装 WordPress 3.0+

这个就不多介绍了，直接按照向导安装即可。我测试的时候是直接用已经安装好的独立站点开启多站点的，不过还是建议全新安装。

### 启用 Network

前面介绍到 MU 里面 Network 有两种形式：1是子域名，2是目录，比如 gkp.com/a 和 gkp.com/b ，可以根据个人喜好选择。我选择的是子目录形式<span style = "color:red;">（后续均为以子目录建立多站点网络内容）</span>。

打开 wp-config.php，将下面这行添加在 <span style = "color:red;">define('WP_DEBUG', false);</span> 之前：

<pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444">define('WP_ALLOW_MULTISITE', true);</pre>

之后就可以在后台的 Tools –> Network 看到网络设置了，在这里输入网络的名字和管理员 Email 等信息，点 Install 安装。

然后<span style = "color:red;">按照向导程序的提示分别将给出的文件内容添加到 wp-config.php 和 .htaccess 两个文件中。</span>至此 WordPress MU 网络的设置就完成了，重新登录后台就可以看到左上方多出了<span style = "color:red;">站点网络</span>相关菜单。

### 导入数据

建议直接在原 blog 使用 export 导出 xml，新 blog 这边用 wordpress importer 导入，支持作者映射和附件下载。

### 调整数据

主要是上传文件位置，比如 example.com/wp-content/uploads/ 之前文章中引用的都是这样的地址，可以直接在导出后修改数据库。

### 独立域名映射

  1. 从主站点后台安装并启用 <a href="https://wordpress.org/plugins/wordpress-mu-domain-mapping/" target="_blank">WordPress MU Domain Mapping</a> 插件；
  2. 在该插件目录复制 sunrise.php 一份到 wp-content 目录；
  3. 修改wp-config.php，在 /\* 好了！请不要再继续编辑。请保存本文件。使用愉快！ \*/ 前面加入一行 define( 'SUNRISE', 'on' );  
    进入主站点后台 设置 -> Domain Mapping 里面输入服务器的 IP 地址（或者是一个 CNAME），设置下是否允许用户自行设置域名映射等选项，然后保存即可。
  4. 主站点后台 设置 -> Domains 里面，或者各个子网站管理员后台的 Tools –>Domain Mapping 里面设置域名了，每个网站支持多个域名映射，需要设置一个 primary 域名，最终所有的域名都重定向到这里。

<span style = "color:red;">查看 Site ID 方法</span>： 主站点 -> 站点 -> 所有站点 ，鼠标放到<span style = "color:red;"> 路径 </span>上去，在浏览器左下角看到链接地址？id=xx。

<span style = "color:red;">###############Tips###############</span>

  1. <span style = "color:blue;">WordPress开启目录形式多站点去掉永久链接前的 blog </span>：wp-config.php 中有一个配置是 define('BLOG\_ID\_CURRENT_SITE', 1);表示Site ID 为 1 的站点为默认博客，这个博客固定链接会加了/blog/，只要将1改为一个不存在的 Site ID 即可，比如8。

### 参考资料：

  1. 官方文档：<a href="http://codex.wordpress.org/zh-cn:创建站点网络" target="_blank">创建站点网络</a>
  2. Gkp's Post：<a href="http://b.gkp.cc/2010/08/04/enable-wordpress-30-mu-function-and-map-domain-for-network-blogs/" target="_blank">WordPress 3.0 MU 设置与独立域名映射</a>
  3. 乌徒帮：<a href="http://www.utubon.com/post/67.html" target="_blank">WordPress开启目录形式多站点去掉永久链接前的blog</a>
  4. 水景一页：<a href="http://cnzhx.net/blog/upgrade-to-wp30-multisite-subdirectory/" target="_blank">升级至WordPress 3.0多站点模式</a>
  5. 水景一页：<a href="http://cnzhx.net/blog/update-to-wordpress-3-0-multisite-problem/" target="_blank">升级到WordPress 3.0多站点模式问题探索</a>