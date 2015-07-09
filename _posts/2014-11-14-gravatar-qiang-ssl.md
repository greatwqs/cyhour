---
title: Gravatar 头像被墙及解决方案
author: 老杨
layout: post
permalink: /gravatar-qiang-ssl.html
categories:
  - 老杨转载
tags:
  - wordpress
---
这两天发现 Gravatar 头像加载不了了，上V后正常。哎，这有啥好<span style = "color:red;">强（现代通假字）</span>的呢？  


解决办法：<span style = "color:red;">调用ssl 头像链接</span>——https还是没被墙的，而且速度还不错，直接调用这个最简单了。如果你的网站启用了ssl则不需要了，否则functions.php 加入如下代码即可。

<pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444">/* 调用ssl 头像链接  */<br />function get_ssl_avatar($avatar) {<br />   $avatar = preg_replace('/.*/avatar/(.*)?s=([d]+)<span style="color:#219">&.*/','&lt;img src="https://secure.gravatar.com/avatar/$1?s=$2" class="avatar avatar-$2" height="$2" width="$2"&gt;',$avatar);</span><br />   return $avatar;<br />}<br />add_filter('get_avatar', 'get_ssl_avatar');</pre>

更多解决办法请看 <a href="http://fatesinger.com/74030" target="_blank">大发</a> OR Google、度娘。