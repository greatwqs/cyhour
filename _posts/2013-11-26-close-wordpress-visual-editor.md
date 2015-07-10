---
title: 关闭WordPress可视化编辑器
author: 老杨
layout: post
permalink: /close-wordpress-visual-editor.html
categories:
  - 信息技术
tags:
  - 可视化编辑器
---
彻底关闭WordPress可视化编辑器，在 functions.php 添加如下代码即可：

<pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444">add_filter('user_can_richedit','__return_false');  </pre>