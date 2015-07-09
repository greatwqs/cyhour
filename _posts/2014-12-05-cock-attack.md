---
title: 贼心不死
author: 大肥羊
layout: post
permalink: /cock-attack.html
categories:
  - 信息技术
tags:
  - 攻击
---
<a href="https://cyhour.com/be-hacked.html" target="_blank">半个多月前被悄无声息的安装了插件</a>，好几天后才发现。重新安装了 WordPress 导入文章数据，一直担心不知道什么时候又被安装什么东西，所以现在时不时会检查一下插件有没多，用户有没多……

前两天，加了段登陆提醒代码，不管登陆成功失败都会发邮件提醒。今天早上，打开邮箱，发现有几十封登陆失败的邮件提醒，看了看都是国外的 IP，没有用户名和密码的。今天啥日子？

![Cock-attack-1][1]

![Cock-attack-2][2]

![Cock-attack-3][3]

![Cock-attack-4][4]

* * *<span style = "color:red;">附上登陆提醒邮件通知代码（需将 xxxxxx@qq.com 换成你接收通知的邮件地址）：</span></p> 

<pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444">/**获取用户真实IP*/<br />function cy_getIP(){<br />	static $realIP;<br />	if (isset($_SERVER)){<br />		if (isset($_SERVER["HTTP_X_FORWARDED_FOR"])){<br />			$realIP = explode(',', $_SERVER["HTTP_X_FORWARDED_FOR"]);<br />			$realIP = $realIP[0];<br />		} else if (isset($_SERVER["HTTP_CLIENT_IP"])) {<br />			$realIP = $_SERVER["HTTP_CLIENT_IP"];<br />		} else {<br />			$realIP = $_SERVER["REMOTE_ADDR"];<br />		}<br />	} else {<br />		if (getenv("HTTP_X_FORWARDED_FOR")){<br />			$realIP = getenv("HTTP_X_FORWARDED_FOR");<br />		} else if (getenv("HTTP_CLIENT_IP")) {<br />			$realIP = getenv("HTTP_CLIENT_IP");<br />		} else {<br />			$realIP = getenv("REMOTE_ADDR");<br />		}<br />	}<br />	$_SERVER['REMOTE_ADDR'] = $realIP;<br />	//return $realIP;<br />}<br />add_action( 'init', 'cy_getIP' );<br /><br />/*根据腾讯IP分享计划的地址获取IP所在地，比较精确*/<br />function getIPLoc_QQ($ip1){<br />	$url = 'http://ip.qq.com/cgi-bin/searchip?searchip1='.$ip1;<br />	$ch = curl_init($url);<br />	curl_setopt($ch,CURLOPT_ENCODING ,'gb2312');<br />	curl_setopt($ch, CURLOPT_TIMEOUT, 10);<br />	curl_setopt($ch, CURLOPT_RETURNTRANSFER, true) ; // 获取数据返回<br />	$result = curl_exec($ch);<br />	$result = mb_convert_encoding($result, "utf-8", "gb2312"); // 编码转换，否则乱码<br />	curl_close($ch);<br />	preg_match("@<span style="color:#170">&lt;span</span><span style="color:#170">&gt;</span>(.*)<span style="color:#170">&lt;/span</span><span style="color:#170">&gt;</span><span style="color:#f00">&lt;/p</span><span style="color:#f00">&gt;</span>@iU",$result,$ipArray);<br />	$loc = $ipArray[1];<br />	return $loc;<br />}<br /><br />/*************登录wp后台成功就会email通知博主************/<br />function wp_login_notify(){<br />	date_default_timezone_set('PRC');<br />	$to = 'xxxxxx@qq.com';<br />	$wp_email = 'no-reply@' . preg_replace('#^www\.#', '', strtolower($_SERVER['SERVER_NAME'])); <br />	$subject = '博客『' . get_option("blogname") . '』登录提醒';<br />	$message = '博客『' . get_option("blogname") . '』有用户登录成功！<span style="color:#170">&lt;br</span><span style="color:#170">/&gt;</span>' . '登录信息如下：<span style="color:#170">&lt;br</span><span style="color:#170">/&gt;</span>' . '登录帐号：' . $_POST['log'] . '<span style="color:#170">&lt;br</span><span style="color:#170">/&gt;</span>' .'登录时间：' . date("Y-m-d H:i:s") . '<span style="color:#170">&lt;br</span><span style="color:#170">/&gt;</span>' .'登录IP：'. $_SERVER['REMOTE_ADDR'] .'【'. getIPLoc_QQ($_SERVER['REMOTE_ADDR']).'】';<br />	$from = "From: \"" . get_option('blogname') . "\" <span style="color:#170">&lt;$wp_email</span><span style="color:#170">&gt;</span>";<br />	$headers = "$from\nContent-Type: text/html; charset=" . get_option('blog_charset') . "\n";<br />	wp_mail( $to, $subject, $message, $headers );<br />}<br />add_action('wp_login', 'wp_login_notify');<br /><br />/*************登录wp后台失败就会email通知博主************/<br />function wp_login_failed_notify(){<br />	date_default_timezone_set('PRC');<br />	$to = 'xxxxxx@qq.com';<br />	$wp_email = 'no-reply@' . preg_replace('#^www\.#', '', strtolower($_SERVER['SERVER_NAME'])); <br />	$subject = '博客『' . get_option("blogname") . '』登录失败警告';<br />	$message = '博客『' . get_option("blogname") . '』有用户登录失败！<span style="color:#170">&lt;br</span><span style="color:#170">/&gt;</span>' . '登录信息如下：<span style="color:#170">&lt;br</span><span style="color:#170">/&gt;</span>' . '登录帐号：' . $_POST['log'] . '<span style="color:#170">&lt;br</span><span style="color:#170">/&gt;</span>' .'登录密码：' . $_POST['pwd'] . '<span style="color:#170">&lt;br</span><span style="color:#170">/&gt;</span>' .'登录时间：' . date("Y-m-d H:i:s") . '<span style="color:#170">&lt;br</span><span style="color:#170">/&gt;</span>' .'登录IP：'. $_SERVER['REMOTE_ADDR'] .'【'. getIPLoc_QQ($_SERVER['REMOTE_ADDR']).'】';<br />	$from = "From: \"" . get_option('blogname') . "\" <span style="color:#170">&lt;$wp_email</span><span style="color:#170">&gt;</span>";<br />	$headers = "$from\nContent-Type: text/html; charset=" . get_option('blog_charset') . "\n";<br />	wp_mail( $to, $subject, $message, $headers );<br />}<br />add_action('wp_login_failed', 'wp_login_failed_notify');</pre>

参考文章：  
http://www.yuxiaoxi.com/2013-07-17-wordpress-login-notification.html

http://blog.gimhoy.com/archives/wordpress-login-notification-with-location-info.html

<span style = "color:red;">小伙伴们，除了安装插件有没啥好的方法防止攻击或者被黑呢？</span>

 [1]: https://cyhour.com/wp-content/uploads/2014/12/Cock-attack-1.png
 [2]: https://cyhour.com/wp-content/uploads/2014/12/Cock-attack-2.png
 [3]: https://cyhour.com/wp-content/uploads/2014/12/Cock-attack-3.png
 [4]: https://cyhour.com/wp-content/uploads/2014/12/Cock-attack-4.png