---
title: Win7连接XP打印机问题
author: 大肥羊
layout: post
permalink: /win7-xp-printer.html
categories:
  - 信息技术
tags:
  - win7
  - 打印机
---
前台又换回昔日的xp老爷机了，打印问题又来了……<span style="color: #0000ff;">每天都有人在叫：又打印不了了</span>。搞得心烦意乱啊。

> Google了一下【针对打印机连接在XP系统上所出现的问题的解决方案】
> 
> 1、 XP系统的设置  
> 控制面板 → 管理工具 → 本地安全策略 → 本地策略 → 用户权限分配，在【从网络访问计算机】里面添加Guest用户，并且在【拒绝从网络访问计算机】里面删除Guest用户。
> 
> 同时在 控制面板 → 管理工具 → 本地安全策略 → 本地策略 → 安全选项 里面保证 Guest用户处于启用状态。  
> 修改【网络访问】 本地账户的共享和安全模型 的设置为【仅来宾...】 
> 
> 做完以上工作之后XP系统计算机之间已经可以网络打印了。 点击【开始】 → 运行，输入 ip,可以看到目标计算机的共享。 右键点击目标打印机，选择连接即可。 
> 
> 一般按照上面的设置完成，Win7系统也可以连接到XP的共享的打印机了，如果不行再按第二点设置一下Win7就可以了。
> 
> 2、Win7系统的设置  
> 首先在服务里面把【print splooer】服务改为手动启动。 然后在设备和打印机里面选择添加打印机 → 添加本地打印机 → 创建新端口 → Local port，输入打印机的绝对路径 ip打印机共享名，如192.168.11.17hp 选择打印机驱动，如果系统没有的话选择从磁盘安装，然后下一步直至完成。有时下一步会不行，多点两次就OK。 最后再把print splooer服务改回自动启动。 
> 
> <span style="color: #ff0000;">注意，整个过程当中print splooer服务都要保持启动状态。 </span>