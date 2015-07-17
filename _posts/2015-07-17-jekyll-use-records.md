---
Date: 2015-07-17 08:08
title: Jekyll 使用记录
author: 老杨
layout: post
permalink: /jekyll-use-records.html
categories:
  - 信息技术
tags:
  - Jekyll
---
[常阳时光(SYN)](http://syn.cyhour.com) 基本上能正常运行了，趁热打铁，把折腾的一些过程记录一下，算是笔记吧。需要的网友也可以参考一下。PS：可能会有些非常非常业余的代码，所以参考的自己看着办吧。

### `&lt;!--more--&gt;` 标签

我在 WordPress 发布的所有文章，都在第一段后手工加了 `&lt;!--more--&gt;` 标签，这样首页内容能带 html 样式显示（WordPress 自动截断会把样式都去掉，虽然高度看起来统一了，但是内容看起来可能就怪怪的了）。Jekyll 会自动取每篇文章从开头到第一次出现 excerpt_separator 的地方作为文章的摘要。 如果没有配置 excerpt_separator，Jekyll 默认会截取文章第一段作为摘要。我用的是这个方法，所以把 WordPress 导出的文章的 `&lt;!--more--&gt;` 标签批量删除掉了。

如果想自己控制输出多段，可以在需要截断的地方添加 `&lt;!--more--&gt;` 标签，并且在 _config.yml 文件中添加配置：`excerpt_separator: "&lt;!-- more --&gt;"` 。

当然，也可以像 WordPress 那样添加 `&lt;!--more--&gt;` 标签，并添加 Read More 链接。使用下面的代码就可以了，[原文](http://moamaoa.com/jekyll/%E9%A2%84%E8%A7%88%E4%B8%80%E7%AF%87Jekyll%E7%9A%84%E6%96%87%E7%AB%A0%E5%B9%B6%E6%B7%BB%E5%8A%A0Readmore/)。<span style = "color:red;">（没有测试）</span>

<pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444">{% if post.content contains '<span style="color:#a50">&lt;!-- more --&gt;</span>' %}
    {{ post.content | split:'<span style="color:#a50">&lt;!-- more --&gt;</span>' | first }}
    <span style="color:#170">&lt;p</span> <span style="color:#00c">class</span>=<span style="color:#a11">"more"</span><span style="color:#170">&gt;</span><span style="color:#170">&lt;a</span> <span style="color:#00c">href</span>=<span style="color:#a11">"{{ post.url }}"</span><span style="color:#170">&gt;</span>Read More <span style="color:#219">&amp;raquo;</span><span style="color:#170">&lt;/a</span><span style="color:#170">&gt;</span><span style="color:#170">&lt;/p</span><span style="color:#170">&gt;</span>
{% else %}
    {{ post.content }}
{% endif %}</pre>

详细请参考：[官方文档](http://jekyllrb.com/docs/posts/#post-excerpts)

### 分页功能

Jekyll 目前只能对首页进行分页，分类/标签下的文章无法分页，如有方法能实现，请留言告知，谢谢。

开启分页功能很简单，只需要在 _config.yml 里面添加一行 paginate 配置每页显示多少篇文章即可。如，每页最多显示 8 篇文章，添加如下代码即可。

`paginate: 8`

下面我的分页代码，修改自：[V2EX](https://www.v2ex.com/t/32433#r_438085)，代码放到 index.html 恰当位置即可。

<pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444">  <span style="color:#170">&lt;div</span> <span style="color:#00c">id</span>=<span style="color:#a11">"post-pagination"</span> <span style="color:#00c">class</span>=<span style="color:#a11">"pagination"</span><span style="color:#170">&gt;</span>
    {% if paginator.page == 1 %}
      <span style="color:#170">&lt;span</span> <span style="color:#00c">class</span>=<span style="color:#a11">"page-numbers current"</span><span style="color:#170">&gt;</span>1<span style="color:#170">&lt;/span</span><span style="color:#170">&gt;</span>
    {% else %}
      <span style="color:#170">&lt;a</span> <span style="color:#00c">class</span>=<span style="color:#a11">"page-numbers"</span> <span style="color:#00c">href</span>=<span style="color:#a11">"/"</span><span style="color:#170">&gt;</span>1<span style="color:#170">&lt;/a</span><span style="color:#170">&gt;</span>
    {% endif %}

    {% assign pageSize = 2 %}
    {% assign startPage = paginator.page | minus:pageSize %}
    {% if 2 &gt; startPage %}
      {% assign startPage = 2 %}
    {% endif %}
    {% assign endPage = paginator.page | plus:pageSize %}
    {% if endPage &gt;= paginator.total_pages %}
      {% assign endPage = paginator.total_pages | minus:1 %}
    {% endif %}

    {% assign pageTemp = pageSize | plus:2 %}
    {% if paginator.page &gt; pageTemp %}
      <span style="color:#170">&lt;span</span> <span style="color:#00c">class</span>=<span style="color:#a11">"page-numbers dots"</span><span style="color:#170">&gt;</span>…<span style="color:#170">&lt;/span</span><span style="color:#170">&gt;</span>
    {% endif %}

    {% for count in (startPage..endPage) %}
      {% if count == paginator.page %}
        <span style="color:#170">&lt;span</span> <span style="color:#00c">class</span>=<span style="color:#a11">"page-numbers current"</span><span style="color:#170">&gt;</span>{{ count }}<span style="color:#170">&lt;/span</span><span style="color:#170">&gt;</span>
      {% else %}
        <span style="color:#170">&lt;a</span> <span style="color:#00c">class</span>=<span style="color:#a11">"page-numbers"</span> <span style="color:#00c">href</span>=<span style="color:#a11">"/page{{ count }}"</span><span style="color:#170">&gt;</span>{{ count }}<span style="color:#170">&lt;/a</span><span style="color:#170">&gt;</span>
      {% endif %}
    {% endfor %}

    {% assign pageTemp1 = pageSize | plus:1 %}
    {% assign pageTemp = paginator.page | plus:pageTemp1 %}
    {% if paginator.total_pages &gt; pageTemp %}
      <span style="color:#170">&lt;span</span> <span style="color:#00c">class</span>=<span style="color:#a11">"page-numbers dots"</span><span style="color:#170">&gt;</span>…<span style="color:#170">&lt;/span</span><span style="color:#170">&gt;</span>
    {% endif %}

    {% if paginator.page == paginator.total_pages %}
      <span style="color:#170">&lt;span</span> <span style="color:#00c">class</span>=<span style="color:#a11">"page-numbers current"</span><span style="color:#170">&gt;</span>{{paginator.total_pages}}<span style="color:#170">&lt;/span</span><span style="color:#170">&gt;</span>
    {% else %}
      <span style="color:#170">&lt;a</span> <span style="color:#00c">class</span>=<span style="color:#a11">"page-numbers"</span> <span style="color:#00c">href</span>=<span style="color:#a11">"/page{{paginator.total_pages}}/"</span><span style="color:#170">&gt;</span>{{paginator.total_pages}}<span style="color:#170">&lt;/a</span><span style="color:#170">&gt;</span>
    {% endif %}

  <span style="color:#170">&lt;/div</span><span style="color:#170">&gt;</span></pre>

参考 CSS：

<pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444"><span style="color:#a50">/*分页*/</span>
.<span style="color:#170">pagination</span> {<span style="color:#000">font-size</span>: <span style="color:#164">14px</span>;<span style="color:#000">margin-top</span>: <span style="color:#164">18px</span>; <span style="color:#000">text-align</span>: <span style="color:#164">center</span>; }
.<span style="color:#170">pagination</span> .<span style="color:#170">page-numbers</span>{<span style="color:#000">color</span>:<span style="color:#219">#111</span>;<span style="color:#000">display</span>: <span style="color:#164">inline-block</span>;<span style="color:#000">text-align</span>: <span style="color:#164">center</span>;<span style="color:#000">width</span>: <span style="color:#164">24px</span>;<span style="color:#000">line-height</span>:<span style="color:#164">24px</span>;<span style="color:#000">margin</span>:<span style="color:#164">5px</span>;<span style="color:#000">background</span>: <span style="color:#219">#E4E5E1</span>;}
.<span style="color:#170">pagination</span> .<span style="color:#170">page-numbers</span>.<span style="color:#170">current</span>{ <span style="color:#000">background</span>: <span style="color:#219">#c30</span>;<span style="color:#000">color</span>:<span style="color:#219">#fff</span>;}	
.<span style="color:#170">pagination</span> .<span style="color:#170">page-numbers</span>.<span style="color:#170">dots</span>{<span style="color:#000">border-color</span>:<span style="color:#164">rgba</span><span style="color:#164">(0</span>,<span style="color:#164">0</span>,<span style="color:#164">0</span>,<span style="color:#164">0</span><span style="color:#164">)</span>}</pre>

效果如下图，修改` pageSize `值即可控制当前页前后输出的页码数。

![ pagination-demo-jekyll ](//cyhour.com/wp-content/uploads/2015/07/pagination-demo-jekyll.png)

详细参考：[官方文档](http://jekyllrb.com/docs/pagination/)、[非官方中文（翻译不是很准确）](http://jekyllcn.com/docs/pagination/)。

### 分类 & 标签功能

Jekyll 的分类和标签功能没有 WordPress 完善，凑合着用吧。

模板代码和样式参考自：[谢益辉](http://yihui.name/cn/) & [天涯孤鸟](http://cnitzone.com/)。

### 评论

必须得用第三方评论系统，这个是最大的硬伤，若不是，我可能彻底投奔 Jekyll 了。 国外的 Disqus 感觉更有节操，不过国内加载实在是太慢了。所以放弃了 [Disqus + 多说](http://dlyang.me/two-comment-plugins) 两种评论框一起用。

### RSS

代码来自：[jekyll-rss-feeds](https://github.com/snaptortoise/jekyll-rss-feeds)，只针对个人模板配置小改了一下——`site.name` 改为 `site.title`，需根据个人配置修改。

代码就不贴了，需要的可以到 Github 看源文件。

### sitemap

对于 sitemap，WordPress 是安装插件解决的，Jekyll 好像也可以安装插件解决，比如：[jekyll-sitemap](https://github.com/jekyll/jekyll-sitemap)，不过我是没有折腾成功。如果你愿意，也可以试试这个[插件](https://github.com/kinnetica/jekyll-plugins)。

不过我现在用的是免插件方法：[Generating a Sitemap in Jekyll without a Plugin](https://github.com/havvg/havvg.github.com/blob/master/sitemap.xml)

### SEO 优化

这个不大懂，目前只优化了一下网页 title，分页加上了"第 xx 页"字样。用下面的代码替换掉原始的 <head>……</head> 之间的 title 代码即可。

<pre style="margin:15px 0;font:100 12px/18px monaco, andale mono, courier new;padding:10px 12px;border:#ccc 1px solid;border-left-width:4px;background-color:#fefefe;box-shadow:0 0 4px #eee;word-break:break-all;word-wrap:break-word;color:#444">    <span style="color:#170">&lt;title</span><span style="color:#170">&gt;</span>
        {% if page.title %}{{ page.title | strip_html }} <span style="color:#219">&amp;#8211;</span> {% endif %}
        {{ site.title | strip_html }}
        {% if paginator.page &gt; 1 %}
          <span style="color:#219">&amp;#8211;</span> 第 {{ paginator.page | strip_html }} 页
        {% endif %}
        {% if page.layout == 'default' %}<span style="color:#219">&amp;#8211;</span> {{ site.description | strip_html }} {% endif %}
    <span style="color:#170">&lt;/title</span><span style="color:#170">&gt;</span></pre>

    未完，待更新！