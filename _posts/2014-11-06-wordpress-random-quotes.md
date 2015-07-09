---
title: WordPress 随机显示名人格言
author: 老杨
layout: post
permalink: /wordpress-random-quotes.html
categories:
  - 信息技术
tags:
  - 名言格言
---
在 <a href="http://program-think.blogspot.com/" target="_blank">编程随想</a> <span style = "color:red;">（需梯子）</span>的博客看到个不错的功能——随机显示博主精选的名人格言，稍稍折腾，我也加上了这功能了（在首页随机显示我喜欢的句子）。 <img src="http://cyhour.com/wp-includes/images/smilies/icon_razz.gif" alt=":razz:" class="wp-smiley" />  


网上（官网的是英文版的格言）有现成的插件，<a href="http://xinple.org/?p=37" rel="nofollow" target="_blank">传送门</a>。一个很简单的插件，其实可以集成到 functions.php 去。不过格言也存放在插件的php文件里面，集成到 functions.php 里面可能就很乱了，还是单独一个插件比较好。

插件下载：<a href="/wp-content/uploads/2014/11/random-quotes.zip" target="_blank">random-quotes</a>

使用方法：

  1. 安装并激活该插件
  2. 在需要显示的地方调用： <pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444"><span style="color:#555">&lt;?php</span> <span style="color:#708">if</span>(<span style="color:#@cm-word">function_exists</span>(<span style="color:#a11">'show_quotes'</span>)) <span style="color:#@cm-word">show_quotes</span>(); <span style="color:#555">?&gt;</span></pre>

  3. 根据需要调整css
  4. 可以在 random-quotes.php 文件的 $quotes = <<< eot 后面添加自己喜欢的句子（中英文皆可），一句一行。

完！