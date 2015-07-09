---
title: 流量就是这样溜走的
author: 大肥羊
layout: post
permalink: /liuliangjiushizheyangliuzoude.html
categories:
  - 其它分类
tags:
  - 垃圾评论
  - 流量
---
自从用上了大发的【WordPress对比Gravatar头像md5拦截垃圾评论】，评论一直冷冷清清的，而最近两个月发现，流量跑得巨快，而访问量就那么的一点点点。。。



今天，流量就快没了。把数据库清了，wordpress重新安装了。

然后，试着把下面的拦截代码去掉，待审核的评论噼里啪啦就来了，原来流量就是那样一点一点被耗掉了！

<pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444">// WordPress对比Gravatar头像md5拦截垃圾评论  <br />function cy_spam( $comment ) {    <br />     $email = $comment['comment_author_email'];    <br />     $g = 'http://www.gravatar.com/avatar/'. md5( strtolower( $email ) ). '?d=404';    <br />     $headers = @get_headers( $g );    <br />         if ( !preg_match("|200|", $headers[0]) ) {    <br />         die();    <br />      }        <br />     return $comment;    <br />}    <br />add_action('preprocess_comment', 'cy_spam');  </pre>

代码去掉了大概10分钟，待审的评论就300+了，并且不停的在刷新。。。

![lajipinglun][1]

想用.htaccess限制一下某些ip访问，却发现一点用都没有。把wp-comment-post.php干掉了，仍然没有效果，难道只能CDN挡一下？

可恶的垃圾。。。

 [1]: https://cyhour.com/wp-content/uploads/2013/11/lajipinglun.jpg