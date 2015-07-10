---
title: DirectAdmin安装StartSSL免费SSL证书
author: 老杨
layout: post
permalink: /directadmin-install-startssl-free-ssl-certificates.html
categories:
  - 信息技术
tags:
  - StartSSL 免费证书
---
DirectAdmin安装StartSSL免费SSL证书，大致步骤是：注册StartSSL -> 验证域名 -> 申请证书【分为两步，生成私匙（可在DirectAdmin控制面板生成，也可以直接在StartSSL中生成） 和 生成证书 】 -> 在DirectAdmin安装证书 -> WordPress 配置 https。  


  
下面是方法：

### 1、注册StartSSL

这个就不多说了，网上有很多现成的教程，也不难，主要是信息填写正确就可以了，我是申请了两次就通过了。附上<a href="http://www.freehao123.com/startssl-ssl/" target="_blank" rel="nofollow">免费资料部落注册StartSSL的教程</a>。

### 2、验证域名

这个也简单，验证时，把域名注册E-mail收到的验证码填入认证即可。<span style = "color:red;">注意：</span>如设置了域名隐私保护，需要先关闭隐私保护。

![ Select-Validation ][1]

![ Enter-Domain-Name ][2]

![ Select-Verification-Email ][3]

![ Complete-Validation ][4]

![ Validation-Success ][5]

### 3、申请证书

分为<span style = "color:blue;">生成私匙</span>（可在DirectAdmin控制面板生成，也可以直接在StartSSL中生成） 和 <span style = "color:blue;">生成证书</span>两步。

我是直接在StartSSL中生成私匙的，生成私匙 和 生成证书在Certificates Wizard就可以完成。

![ Certificates-Wizard ][6]

a.->选择 <span style = "color:blue;">Web Server SSL/TLS Certiticate</span> ，然后 Continue 即可。

b.->生成私匙（Generate Private Key），输入密匙加密密码（注意保存密码），点击 Continue，弹出的提示框按确定即可。<span style = "color:red;">（如已在DirectAdmin控制面板生成私匙，点 Skip 跳过此步）</span>

![ StartSSL-Generate-Private-Key ][7]

c.->保存私匙（Save Private Key），保存到 txt 文件或者另存为 ssl.key ，然后 Continue。

![ Save-Private-Key ][8]

d.->添加域名（Add Domains），然后还要添加一个子域名，一般写 www 即可。--> Continue。 

![ Add-Domains ][9]

![ add-one-sub-domain ][10]

Continue 转到准备生成证书页面，--> Continue。

![ Ready-Processing-Certificate ][11]

证书生成了，保存为 txt 文件或者 ssl.crt。另外，下图红色横线上面的两个链接文件（ Intermediate 和 root CA）也要另存下来。

![ Save-Certificate ][12]

<span style = "color:red;">至此证书申请完毕！</span>

附上：DirectAdmin控制面板生成私匙方法。

![ DirectAdmin-Generate-Private-Key ][13]

![ DirectAdmin-Generate-Private-Key ][14]

### 4、在DirectAdmin安装证书

a.在 DirectAdmin 选择要配置SSL的域名，点SSL证书开启改域名【安全的SSL】。

![ start-SSL-DA ][15]

![ Open-SSL-DA ][16]

b.私匙到StartSSL解密（如私匙在DirectAdmin生成的则不用），Tool Box -> Decrypt Private Key，将前面生成的ssl.key私匙和密码分别输入到框内。

![ Decrypt-Private-Key ][17] 

c.点 Decrypt 完成解密，将解密后的私匙 与 前面生成的证书ssl.crt 一起粘贴到DirectAdmin控制面板，然后保存即可。

![ DA-Install-Certificate ][18] 

d.粘贴 CA 根证书到 DirectAdmin控制面板。

将生成证书最后一步 <span style = "color:red;">Intermediate</span> 链接保存的文件内容粘贴到上图左下角<span style = "color:red;">[点击此处 粘贴CA根证书]</span>处即可。

![ Root-CA-SSL ][19] 

<span style = "color:red;">至此，证书安装完毕。</span>

### 5、WordPress 整站 HTTPS 免插件配置

<span style = "color:red;">0.0.配置 HTTPS 的前提条件</span>

  * 最好是 VPS 甚至独立服务器，如果是共享主机的，则需要主机商提供 SSL/TLS 功能。
  * 服务器上必须开启了 mod_ssl。
  * 必须独立 IP，如果没有，则需要主机打开 SNI 功能，比如<span style = "color:blue;">兔二爷</span>推荐的 <a href="https://too2ye.com/3002" target="_blank">MediaTemple GRID主机</a>。

a.更改【WordPress地址（URL）】和【站点地址（URL）】为 https 链接。（仪表盘->设置->常规）

![ WordPress-Sites-URL ][20] 

b.进数据库，SQL替换文章内容、评论内容中的http链接（操作数据库有风险，注意备份）

<pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444">UPDATE wp_posts SET post_content = REPLACE (post_content, 'http://www.example.com', 'https://www.example.com');   <br />UPDATE wp_posts SET post_content = REPLACE (post_content, 'http://example.com', 'https://example.com');   <br /></pre>

<pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444">UPDATE wp_comments SET comment_content = REPLACE( comment_content, 'http://cyhour.com/', 'http://cyhour.com/' );<br />UPDATE wp_comments SET comment_content = REPLACE( comment_content, 'http://www.cyhour.com/', 'https://www.cyhour.com/' );</pre>

c. 配置 .htaccess 整站 http 强制跳转到 https。（据说此方法可以照顾度娘收录）更详细方法移步【<a href="https://wzyboy.im/post/799.html" target="_blank">Wzyboy’s Blog</a>】

<pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444">RewriteEngine On<br />RewriteCond %{HTTPS} !on [NC]<br />RewriteCond %{HTTP_USER_AGENT} !(baiduspider|soso|bing|sogou|yahoo|sohu-search|yodao|robozilla|msnbot|msie|feedburner) [NC]<br />RewriteRule (.*) https://example.com%{REQUEST_URI} [R=301,NC,L]</pre>

注意此代码可能需要放至 WordPress 伪静态配置代码前面，比如：

<pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444"># BEGIN WordPress<br /><span style="color:#170">&lt;IfModule</span> <span style="color:#00c">mod_rewrite.c</span><span style="color:#170">&gt;</span><br />RewriteEngine On<br />RewriteCond %{HTTPS} !on [NC]<br />RewriteCond %{HTTP_USER_AGENT} !(baiduspider|soso|bing|sogou|yahoo|sohu-search|yodao|robozilla|msnbot|msie|feedburner) [NC]<br />RewriteRule (.*) http://cyhour.com%{REQUEST_URI} [R=301,NC,L]<br />RewriteBase /<br />RewriteRule ^index\.php$ - [L]<br />RewriteCond %{REQUEST_FILENAME} !-f<br />RewriteCond %{REQUEST_FILENAME} !-d<br />RewriteRule . /index.php [L]<br /><span style="color:#170">&lt;/IfModule</span><span style="color:#170">&gt;</span><br /># END WordPress</pre>

d.手工检查将主题、评论、插件等引用的http改为https

至此已基本完成了 WordPress 整站 https 了。

\---\---\---\---\---\---\---\---\---\---\---\---\-----  
吐槽：修改了 DNS 服务器，等了小半天终于切换过来了。（ 修改 DNS 服务器需要最长 48 小时的全球生效时间，请耐心等待）

<span style = "color:red;">\---\---\---\---\-----后记\---\---\---\---\---\---</span>  
HTTPS 昨晚才基本弄好，Google 搜索首页几乎是秒变，度娘的暂时也还能搜索到。

![ Google-Https-SSL-cyhour ][21]

![ Baidu-Https-SSL-cyhour ][22]

 [1]: /wp-content/uploads/2014/12/Select-Validation.png
 [2]: /wp-content/uploads/2014/12/Enter-Domain-Name.png
 [3]: /wp-content/uploads/2014/12/Select-Verification-Email.png
 [4]: /wp-content/uploads/2014/12/Complete-Validation.png
 [5]: /wp-content/uploads/2014/12/Validation-Success.png
 [6]: /wp-content/uploads/2014/12/Certificates-Wizard.png
 [7]: /wp-content/uploads/2014/12/StartSSL-Generate-Private-Key.png
 [8]: /wp-content/uploads/2014/12/Save-Private-Key.png
 [9]: /wp-content/uploads/2014/12/Add-Domains.png
 [10]: /wp-content/uploads/2014/12/add-one-sub-domain.png
 [11]: /wp-content/uploads/2014/12/Ready-Processing-Certificate.png
 [12]: /wp-content/uploads/2014/12/Save-Certificate.png
 [13]: /wp-content/uploads/2014/12/DirectAdmin-Generate-Private-Key-1.png
 [14]: /wp-content/uploads/2014/12/DirectAdmin-Generate-Private-Key-2.png
 [15]: /wp-content/uploads/2014/12/start-SSL-DA.png
 [16]: /wp-content/uploads/2014/12/Open-SSL-DA.png
 [17]: /wp-content/uploads/2014/12/Decrypt-Private-Key.png
 [18]: /wp-content/uploads/2014/12/DA-Install-Certificate.png
 [19]: /wp-content/uploads/2014/12/Root-CA-SSL.png
 [20]: /wp-content/uploads/2014/12/WordPress-Sites-URL.png
 [21]: http://cyhour.com/wp-content/uploads/2014/12/Google-Https-SSL-cyhour.png
 [22]: http://cyhour.com/wp-content/uploads/2014/12/Baidu-Https-SSL-cyhour.png