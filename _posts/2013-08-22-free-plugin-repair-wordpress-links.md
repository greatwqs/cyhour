---
title: 免插件修复WordPress友情链接功能
author: 老杨
layout: post
permalink: /free-plugin-repair-wordpress-links.html
categories:
  - 信息技术
tags:
  - wordpress
  - 友情链接
---
WordPress从3.5版本开始已经移除了链接管理功能（<span style="color: #0000ff;">当然，如果你的WordPress是从旧版本升级的话你会发现还会有链接管理功能</span>）。如果想要激活该功能的话，官方推荐是安装一款插件 Link-manager。但实际上，一行代码就可以搞定。  


  
将下面的代码添加到<span style="color: #0000ff;">主题的funtions.php</span> 文件的<span style="color: #ff0000;"><?php  ?> </span>内，就可以实现链接管理功能了。

<pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444">add_filter( 'pre_option_link_manager_enabled', '__return_true' ); </pre>