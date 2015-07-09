---
title: OpenWRT用AP+WDS模式搭建无线中继
author: 老杨
layout: post
permalink: /openwrt-ap-wds-wireless-repeater.html
categories:
  - 信息技术
tags:
  - OpenWRT
  - 无线中继
---
两个路由器分别配置为：AP1设置为Access Point+WDS模式，AP2设置为Client和AP模式。实现AP2通过无线与AP1连接，然后将AP1的网络通过AP2的无线和有线LAN口共享出去。  


  
我用的是2台刷好OPENWRT的TPLink路由器：<a href="/tl-wr720n-tl-wr743n-upgrade-openwrt.html" target="_blank">TL-WR720N和TL-WR743N</a>。

TL-WR720N 放在客厅，作为主AP（AP1）；TL-WR743N 放在卧室，作为中继AP（AP2）。其实AP2一般是用不上的，纯折腾，备用。下面是折腾LOG：

<span style="color: #ff0000;">AP1（主）的配置</span>：1.DHCP开启；2.无线Mode选择AP+WDS；3.固定信道。参考下图：

![main_wireless_setting][1]

<span style="color: #ff0000;">AP2（客）的配置</span>：1. 关闭DHCP；2.两个无线Mode分别选择Client（WDS）和AP。<span style="color: #ff0000;">两路由器网段不能相同（如我AP1设为192.168.1.1，AP2设为192.168.2.1网段）</span>。

1、登录AP2，打开 网络->无线 界面。在无线概况的 Wireless Controller (radio0) （固件不一样这里显示的名字也可能不一样）里点击 <span style="color: #0000ff;">搜索</span> ，找到AP1然后输入密码连接（就像手机连接wifi一样）。信道固定为与AP1一样。

![about_wireless][2]

2、连接后，添加一个AP模式的无线设备，在无线概况的 Wireless Controller (radio0)里，点击 添加 即可。模式设置成“接入点AP”，网络选择“LAN”。AP名字和密码按需要设定。然后保存和应用。

下图为概览的无线配置状况：

![repeater_setting][3]

<span style="color: #0000ff;">到此为止，如无意外，你应该可以用AP2的无线上网了。</span>

<span style="color: #ff0000;">ZWW大叔提醒：两个路由无线SSID、加密方式、密码、信道都配置成相同的，可以实现无线无缝漫游。（亲测可用）</span>

如无法中继成功（无线不能上网），用<a href="/tl-wr720n-tl-wr743n-upgrade-openwrt.html" target="_blank">WinSCP工具</a>登录中继路由器。打开/etc/config/wireless文件，根据实际情况修改里面的配置，保存，重启路由器即可。<span style="color: #ff0000;">附上参考配置，其中红色字体为说明，不能拷贝到配置文件中。</span>

config wifi-device 'radio0'  
　　　　option type 'mac80211'  
　　　　option macaddr '14:e6:e4:e2:ee:40'  
　　　　option hwmode '11ng'  
　　　　option htmode 'HT20'  
　　　　list ht_capab 'SHORT-GI-20'  
　　　　list ht_capab 'SHORT-GI-40'  
　　　　list ht_capab 'RX-STBC1'  
　　　　list ht\_capab 'DSSS\_CCK-40'  
　　　　option noscan '1'  
　　　　option txpower '27'  
　　　　option country 'US'  
　　　　option channel '11' <span style="color: #ff0000;">——信道为11，与AP1一致。</span>  
　　　　option disabled '0'

config wifi-iface <span style="color: #ff0000;">——客户端AP（WDS）模式连接AP1</span>  
　　　　option ssid 'AP1'  
　　　　option encryption 'psk2'  
　　　　option device 'radio0'  
　　　　option mode 'sta'  
　　　　option wds '1'  
　　　　option network 'wwan'  
　　　　option key '12345678'<span style="color: #ff0000;">——AP1密码</span>

config wifi-iface  
　　　　option device 'radio0'  
　　　　option network 'lan'  
　　　　option disabled '0'  
　　　　option mode 'ap'  
　　　　option ssid 'AP2'  
　　　　option encryption 'psk2'  
　　　　option key '22446688'<span style="color: #ff0000;">——AP2密码</span>

参考1：[无线] openwrt系统用AP+WDS模式搭建无线中继详细教程 http://www.openwrt.org.cn/bbs/forum.php?mod=viewthread&#038;tid=9504&#038;fromuid=53382

参考2：[OpenWRT] RG100A刷OpenWrt超简单万能中继教程 http://forum.anywlan.com/thread-173666-1-1.html

 [1]: http://cyhour.com/wp-content/uploads/2014/03/main_wireless_setting.png
 [2]: http://cyhour.com/wp-content/uploads/2014/03/about_wireless.png
 [3]: http://cyhour.com/wp-content/uploads/2014/03/repeater_setting.png