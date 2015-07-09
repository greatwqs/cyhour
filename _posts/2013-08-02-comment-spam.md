---
title: WordPress对比Gravatar头像md5拦截垃圾评论
author: 老杨
layout: post
permalink: /comment-spam.html
categories:
  - 信息技术
tags:
  - 垃圾评论
---
垃圾评论,很烦人。

每天都有那么几十条无Gravatar头像的国际语言长评论，Trackback的也不少，都要手工标记一下垃圾评论，相当的不爽。又不想用Akismet。  


  
想想还是禁用Trackback，用上大发的【WordPress对比Gravatar头像md5拦截垃圾评论】会省事点，虽然会误Kill好人。对于那些被误Kill的，只能说声Sorry了，因为无法挽救。

代码（来自<a title="大发" href="http://fatesinger.com" target="_blank" rel="external nofollow">大发</a>）如下，直接扔到主题的functions.php中就可以了。只适用于WP。

<pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444">function cy_spam( $comment ) {  <br />    $email = $comment['comment_author_email'];  <br />    $g = 'http://www.gravatar.com/avatar/'. md5( strtolower( $email ) ). '?d=404';  <br />    $headers = @get_headers( $g );  <br />        if ( !preg_match("|200|", $headers[0]) ) {  <br />        die();  <br />    }      <br />    return $comment;  <br />    }  <br />add_action('preprocess_comment', 'cy_spam');</pre>

没有头像的直接咔嚓掉了。

没有头像的同学可以到 <a title="Gravatar官网" href="http://en.gravatar.com/" target="_blank" rel="external nofollow">[ Gravatar官网 ]</a> 申请一个，不懂的可以请教度娘，其实不难。

\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\----  
**PS：实践证明，世界清静了很多~**

可与 【<a href="/to-intercept-spam-without-plugin.html" target="_blank">无需插件实现拦截无中文垃圾评论</a>】配合使用。