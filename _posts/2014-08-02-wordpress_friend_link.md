---
title: WordPress友情链接标识
author: 老杨
layout: post
permalink: /wordpress_friend_link.html
categories:
  - 老杨转载
tags:
  - wordpress
---
在 <a href="http://fatesinger.com/417" rel="external nofollow" target="_blank">大发</a> 那看到的，顺手折腾了一个。<span style="color: #0000ff;">大发</span>说：这个方法是自动给友情链接增加标识，对比友链中的网址，只要评论者提交的网站在友链中就会出现标志。由于采用了超全局变量，也不会增加额外数据库查询次数，效率较高。效果看国旗后面的：<a href="/can-you-tell-me-what-are-uploading.html" target="_blank">GO</a>！  


  
把下面的代码丢主题的functions.php里面去。

<pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444">/*Globals*/<br />global $links;<br />add_action("init","init_globals");<br />function init_globals(){<br />    global $links;<br />    $bookmarks = get_bookmarks();<br />    $links = array();<br />    if ( !empty($bookmarks) ) {<br />        foreach ($bookmarks as $bookmark) {<br />            $url = $bookmark-&gt;link_url;<br />            $url = rtrim($url,"/");<br />            array_push($links,$url);<br />        }<br />    }<br />}<br />/*Globals*/<br />function is_friend_link($url){<br />    $url = rtrim($url,"/");<br />    if(in_array($url,$GLOBALS["links"])){<br />        echo '我是友链';//这里是你的输出内容，你可以写入文字或者图片<br />    }<br />    return false;<br />}</pre>

在你想显示的地方插入，一般是在回调函数中 

<pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444"><span style="color:#555">&lt;?php</span> <span style="color:#@cm-word">is_friend_link</span>(<span style="color:#000-2">$comment</span><span style="color:#000">-&gt;</span><span style="color:#@cm-word">comment_author_url</span>);<span style="color:#555">?&gt;</span></pre>

大发：http://fatesinger.com/417