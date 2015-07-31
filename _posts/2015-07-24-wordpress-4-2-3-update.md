---
Date: 2015-07-24 16:16:00
title: WordPress 4.2.3 Update
author: 老杨
layout: post
permalink: /wordpress-4-2-3-update.html
categories:
  - 信息技术
tags:
  - WordPress
---
小手一抖，已是 WordPress 4.2.3。据说这个版本是关键安全更新，修复了跨站点脚本漏洞。WordPress 4.2.2 及更早版本都受到一个关键的跨站点脚本漏洞，该漏洞可能允许匿名用户操作站点。

用上度娘云加速有好些日子了，另外前些天搬家到[锐壳](http://cyhour.com/out/rkidc)了，望锐壳和度娘能挺住攻击。感谢……

<!-- more -->

主题简单优化了一下，增加了【延迟发送邮件回复 - [BY 木木木木木](http://immmmm.com/comment-mail-schedule.html)】，@ 回复的速度感觉快了那么一点。快来试试吧。

木木给的代码如下，根据自己的模板修改一下就好了：

<pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444">add_action('comment_post','comment_mail_schedule');
function comment_mail_schedule($comment_id){
    //延迟 10s 发送邮件
    wp_schedule_single_event( time()+10, 'comment_mail_event',array($comment_id));
}
add_action('comment_mail_event','ludou_comment_mail_notify');

function ludou_comment_mail_notify($comment_id) {//去除了其中一个参数和判断
  $comment = get_comment($comment_id);
  if ($comment-&gt;comment_parent != '0') {
    $parent_comment = get_comment($comment-&gt;comment_parent);
    $to = trim($parent_comment-&gt;comment_author_email);
    $subject = '您在 [' . get_option("blogname") . '] 的留言有了新的回复';
    $message = '自己的消息内容';
    $message_headers = "Content-Type: text/html; charset=\"".get_option('blog_charset')."\"\n";
    if($to != '' <span style="color:#219">&amp;&amp; $to != get_bloginfo('admin_email'))</span>
      @wp_mail($to, $subject, $message, $message_headers);
  }
};</pre>