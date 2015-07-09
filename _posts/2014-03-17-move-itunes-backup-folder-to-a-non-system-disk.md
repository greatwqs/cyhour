---
title: 移动iTunes备份文件夹至非系统盘
author: 大肥羊
layout: post
permalink: /move-itunes-backup-folder-to-a-non-system-disk.html
categories:
  - 信息技术
tags:
  - itunes
---
iTunes 备份文件夹默认在C盘（系统盘）下，在软件里是无法移动的。<span style="color: #ff0000;">缺点：</span>可能造成了C盘空间不足的问题；一不小心重装系统了，备份就没了。所以移动iTunes备份文件夹至非系统盘就很有必要了。  


### 方法一：不需要任何工具<span style="color: #ff0000;">（仅适用与Win7，Vista和Xp没有测试）</span>

Win7系统下iTunes的备份文件默认在C盘里，路径 C:Users用户名AppDataRoamingApple ComputerMobileSyncBackup里面。通过连接文件mklink命令可以完成文件夹移动。

  * 将【C:Users用户名AppDataRoamingApple ComputerMobileSync】里的<span style="color: #ff0000;">backup</span>文件夹移动到D盘iTunes文件夹下（<span style="color: #ff0000;">注意：</span><span style="color: #0000ff;">是剪切，不是复制；</span>保持mobilesync文件夹为空；D盘可根据实际情况选择）。
  * 以管理员身份运行cmd，执行 <span style="color: #0000ff;">mklink /J "C:Users用户名AppDataRoamingApple ComputerMobileSyncbackup" "D:iTunesbackup"</span> （<span style="color: #ff0000;">注意空格和冒号，用户名填自己的</span>，然后会得到一个类似于快捷方式的东西）。

这样就可以了。

### 方法二：用junction

<span style="color: #0000ff;">junction</span> 微软官方下载地址：<a href="http://technet.microsoft.com/en-us/Sysinternals/Bb896768.aspx" target="_blank" rel="external nofollow">传送门</a>。下载后解压到计算机上，放到C:Windows目录下面。

<span style="color: #0000ff;">junction</span> 工具是一个“连接”程序，可将一个盘中的一个文件夹在物理上“连接”到其他盘上。例如某应用软件访问“C盘Backup0文件夹”，该文件夹是虚拟的，物理上已经被junction工具“连接”到“D盘Backup1文件夹”。

<span style="color: #ff0000;">注意：</span>junction工具只能在NTFS分区下使用，如果计算机是FAT32分区，要使用convert命令将FAT32分区更改成NTFS分区。

<span style="color: #ff0000;">Win7</span> 系统下iTunes的备份文件默认在C盘里，路径 C:Users用户名AppDataRoamingApple ComputerMobileSyncBackup里面。

<span style="color: #ff0000;">Win xp</span>系统下iTunes的备份文件默认在C盘里，路径 C:Documents and Settings用户名Application DataApple ComputerMobileSyncBackup 。

在使用junction工具之前，一定要将【MobileSync】里的<span style="color: #ff0000;">backup</span>文件夹移动到D盘iTunes文件夹下（<span style="color: #ff0000;">注意：</span><span style="color: #0000ff;">是剪切，不是复制；</span>保持mobilesync文件夹为空；D盘可根据实际情况选择）。

打开CMD，键入命令junction "C:documents and settings用户名application dataapplecomputermobilesyncbackup" "d:iTunesbackup" 。<span style="color: #ff0000;">（XP）</span>

对于Win7 命令为：junction "C:Users用户名AppDataRoamingApple Computermobilesyncbackup" "d:iTunesbackup"

<span style="color: #ff0000;">注意：</span>命令行中的符号"是必须的。

回车后会出现一个对话框，选“agree”，然后出现下面的提示就代表成功了：

Created: c:documents and settings用户名application dataapplecomputermobilesyncbackup Targetted at: d:iTunesbackup

另外，移动iTunes媒体文件夹至非系统盘可参考【<a href="/itunes-use-of-skills.html" target="_blank">iTunes使用技巧</a>】这篇文章。